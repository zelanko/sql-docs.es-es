---
title: Optimización del rendimiento de SQL Server R Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dd12e38e0d1f01cd142cc4c11efe43346dd1f8ce
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715619"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Optimización del rendimiento de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo es el primero de una serie de cuatro artículos que describen la optimización del rendimiento de R Services, en función de dos casos prácticos:

- Pruebas de rendimiento realizadas por el equipo de desarrollo del producto para validar el perfil de rendimiento de las soluciones de R

- Optimización del rendimiento por parte del equipo de ciencia de datos de Microsoft para un escenario específico de aprendizaje automático solicitado por los clientes.

El objetivo de esta serie es proporcionar instrucciones sobre los tipos de técnicas de optimización del rendimiento que son más útiles para ejecutar trabajos de R en SQL Server.

+ En este tema (primero) se proporciona información general sobre la arquitectura y algunos problemas comunes al optimizar las tareas de ciencia de datos.
+ En el segundo artículo se tratan las optimizaciones de hardware y SQL Server específicas.
+ En el tercer artículo se tratan las optimizaciones del código R y los recursos para la operacionalización.
+ En el cuarto artículo se describen los métodos de prueba en detalle y se notifican los hallazgos y las conclusiones.

**Se aplica a:** SQL Server 2016 R Services, SQL Server Machine Learning Services

## <a name="performance-goals-and-targeted-scenarios"></a>Objetivos de rendimiento y escenarios de destino

La característica R Services se presentó en SQL Server 2016 para admitir la ejecución de scripts de R mediante SQL Server. Cuando se usa esta característica, el tiempo de ejecución de R funciona en un proceso independiente del motor de base de datos, pero intercambia los datos de forma segura con el motor de base de datos, usando los recursos del servidor y los servicios que interactúan con SQL Server, como el Launchpad de confianza.

En SQL Server 2017, se anunció la compatibilidad para ejecutar scripts de Python con la misma arquitectura, con un lenguaje adicional que seguir en el futuro.

A medida que crece el número de versiones admitidas y el idioma, es importante que el administrador de la base de datos y el arquitecto de la base de datos conozcan el potencial de contención de recursos debido a trabajos de aprendizaje automático, y que puedan configurar el servidor para que admita las nuevas cargas de trabajo. Aunque mantener el análisis cerca de los datos elimina los movimientos de datos inseguros, también mueve las cargas de trabajo analíticas fuera del equipo portátil del científico de datos y vuelve al servidor que hospeda los datos.

La optimización del rendimiento del aprendizaje automático no es claramente una propuesta de un solo tamaño. Las siguientes tareas comunes pueden tener perfiles de rendimiento muy diferentes:

- Tareas de entrenamiento: crear y entrenar un modelo de regresión frente a entrenar una red neuronal
- Ingeniería de características con R frente a la extracción de características mediante T-SQL
- Puntuación en filas individuales o lotes pequeños, frente a puntuación masiva mediante entradas tabulares
- Ejecutar la puntuación en R frente a la implementación de modelos en producción en SQL Server en procedimientos almacenados
- Modificación del código de R para minimizar la transferencia de datos o quitar las transformaciones de datos costosas
- Habilitar las pruebas automatizadas y el reciclaje de los modelos

Dado que la elección de las técnicas de optimización depende de qué tarea es crítica para su aplicación o caso de uso, los casos prácticos cubren sugerencias de rendimiento generales e instrucciones sobre cómo optimizar para un escenario concreto, la optimización de la puntuación por lotes.

+ **Opciones de optimización individuales en SQL Server**

    En el primer caso práctico de rendimiento, se ejecutaron varias pruebas en un único conjunto de resultados con un solo tipo de modelo. El algoritmo rxLinMod de RevoscaleR se usó para generar un modelo y crear puntuaciones a partir de él, pero el código, así como las tablas de datos subyacentes, se modificaron sistemáticamente para probar el impacto de cada cambio.

    Por ejemplo, en una ejecución de pruebas, se modificó el código de R para que se pueda realizar una comparación entre la ingeniería de características mediante una función de transformación en lugar de realizar un cálculo previo de las características y, a continuación, cargar características desde una tabla. En otra serie de pruebas, el rendimiento del entrenamiento del modelo se comparaba entre el uso de una tabla indizada estándar frente a los datos de una tabla con varios tipos de compresión o nuevos tipos de índices.

+ **Optimización para un escenario específico de puntuación de gran volumen**

    La tarea de aprendizaje automático en el segundo caso práctico implica el procesamiento de muchos currículos enviados para varias posiciones y la búsqueda del mejor candidato para cada puesto de trabajo. El propio modelo de aprendizaje automático se formula como un problema de clasificación binaria: toma una descripción de resume y Job como entrada y genera la probabilidad de cada par de resume-Job. Dado que el objetivo es encontrar la mejor coincidencia, se usa un umbral de probabilidad definido por el usuario para filtrar y obtener solo las buenas coincidencias.

    Para esta solución, el objetivo principal era lograr una baja latencia durante la puntuación. Sin embargo, esta tarea es costosa incluso durante el proceso de puntuación, ya que cada nuevo trabajo debe coincidir con millones de currículos dentro de un período de tiempo razonable. Además, el paso de ingeniería de características produce más de 2000 características por reanudación o trabajo, y tiene un cuello de botella significativo en el rendimiento.

Le recomendamos que revise todos los resultados del primer caso práctico para determinar las técnicas que se aplican a la solución y sopese su impacto potencial.

A continuación, revise los resultados del caso práctico de optimización de puntuación para ver cómo el autor aplicó distintas técnicas y optimizó el servidor para admitir una carga de trabajo determinada.

## <a name="performance-optimization-process"></a>Proceso de optimización del rendimiento

La configuración y la optimización del rendimiento requieren la creación de una base sólida, en la que las optimizaciones de capas están diseñadas para cargas de trabajo específicas:

- Elija un servidor adecuado para hospedar análisis. Normalmente, se prefiere un almacén de datos secundario de informes, un almacenamiento de datos u otro servidor que ya se usa para otros informes o análisis. Sin embargo, en una solución híbrida de procesamiento analítico de transacciones (HTAP), los datos operativos se pueden usar como entrada de R para una puntuación rápida.

- Configure la instancia de SQL Server para equilibrar las operaciones del motor de base de datos y la ejecución del script de R o Python en los niveles adecuados. Esto puede incluir cambiar SQL Server valores predeterminados para la memoria y el uso de CPU, la configuración de la afinidad de NUMA y del procesador, y la creación de grupos de recursos.

- Optimice el equipo servidor para admitir el uso eficaz de los scripts externos. Esto puede incluir el aumento del número de cuentas usadas para la ejecución de scripts externos, la habilitación de la administración de paquetes y la asignación de usuarios a roles de seguridad relacionados.

- Aplicar optimizaciones específicas para el almacenamiento de datos y la transferencia en SQL Server, incluidas las estrategias de indexación y estadísticas, el diseño de consultas y la optimización de consultas, y el diseño de las tablas que se usan para el aprendizaje automático. También puede analizar los orígenes de datos y los métodos de transporte de datos, o modificar los procesos ETL para optimizar la extracción de características.

- Ajuste el modelo analítico para evitar ineficiencias. El ámbito de las optimizaciones que son posibles depende de la complejidad del código de R y de los paquetes y datos que se usan. Las tareas clave incluyen la eliminación de las transformaciones de datos costosas o la descarga de la preparación de datos o las tareas de ingeniería de características de R o Python a procesos ETL o SQL. También puede refactorizar scripts, eliminar instalaciones de paquetes en línea, dividir código R en procedimientos independientes de entrenamiento, puntuación y evaluación, o simplificar el código para que funcione de forma más eficaz como un procedimiento almacenado.

## <a name="articles-in-this-series"></a>Artículos de esta serie

+ [Optimización del rendimiento de R en SQL Server-hardware](../r/sql-server-configuration-r-services.md)

    Proporciona instrucciones para configurar el hardware que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está instalado en y para configurar la instancia de SQL Server con el fin de mejorar la compatibilidad con scripts externos. Es especialmente útil para **los administradores de bases de datos**.

+ [Optimización del rendimiento de R en SQL Server: código y optimización de datos](../r/r-and-data-optimization-r-services.md)

    Proporciona sugerencias específicas sobre cómo optimizar el script externo para evitar problemas conocidos. Es más útil para los **científicos de datos**.

    > [!NOTE]
    > Aunque gran parte de la información de esta sección se aplica a R en general, parte de la información es específica de las funciones analíticas de RevoScaleR. Las instrucciones detalladas de rendimiento no están disponibles para **revoscalepy** y otras bibliotecas de Python compatibles.
    >

+ [Optimización del rendimiento de R en SQL Server-métodos y resultados](../r/performance-case-study-r-services.md)

    Resume los datos que se usaron en los dos casos prácticos, cómo se probó el rendimiento y cómo afectan a las optimizaciones.
