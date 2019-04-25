---
title: SQL Server R Services Performance Tuning - SQL Server Machine Learning Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e547e2cd3c50e020d1164dc2b8aaffb31f4e3cb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641655"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Optimización del rendimiento de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo es el primero de una serie de cuatro artículos que describen la optimización de rendimiento para servicios de R, basado en dos casos prácticos:

- Pruebas de rendimiento realizadas por el equipo de desarrollo de productos para validar el perfil de rendimiento de las soluciones de R

- Optimización del rendimiento por el equipo de ciencia de datos de Microsoft para un escenario de aprendizaje automático específico frecuentemente solicitado por los clientes.

El objetivo de esta serie es ofrecer orientación sobre los tipos de técnicas que son muy útiles para ejecutar trabajos de R en SQL Server de optimización del rendimiento.

+ En este tema (primera) proporciona información general de la arquitectura y algunos problemas comunes para optimizar las tareas de ciencia de datos.
+ El segundo artículo cubre el hardware específico y las optimizaciones de SQL Server.
+ El tercer artículo abarca las optimizaciones de código de R y recursos de operacionalización.
+ El cuarto artículo describe los métodos de prueba en detalle y resultados de informes y conclusiones.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="performance-goals-and-targeted-scenarios"></a>Objetivos de rendimiento y los escenarios de destino

La característica R Services se introdujo en SQL Server 2016 para admitir la ejecución de scripts de R con SQL Server. Al usar esta característica, el runtime de R funciona en un proceso independiente desde el motor de base de datos, pero intercambia datos de forma segura con el motor de base de datos, utilizando los recursos del servidor y los servicios que interactúan con SQL Server, como Trusted Launchpad.

En SQL Server 2017, se anunció la compatibilidad para ejecutar scripts de Python con la misma arquitectura, lenguaje adicional para seguir en el futuro.

A medida que crece el número de versiones y de idioma, es importante que el Administrador de base de datos y el arquitecto de base de datos sean conscientes de las posibilidades de contención de recursos debido a trabajos de machine learning, y que se les permite configurar el servidor para admitir las cargas de trabajo nueva. Aunque mantener análisis cerca de los datos elimina los movimientos de datos no seguro, también se mueve las cargas de trabajo analíticos desactivar el equipo portátil de los científicos de datos y vuelva a iniciarla en el servidor que hospeda los datos.

Optimización del rendimiento para el aprendizaje automático no es claramente una propuesta única. Las siguientes tareas comunes que tenga los perfiles de rendimiento muy diferentes:

- Tareas de aprendizaje: crear y entrenar un modelo de regresión frente a entrenar una red neuronal
- Diseño de características con R frente a la extracción de características con Transact-SQL
- Puntuación en filas individuales o en lotes pequeños, frente a masiva con entradas de tabla de puntuación
- Ejecución de R de puntuación frente a implementación de modelos en producción en SQL Server en los procedimientos almacenados
- Modificar el código de R para minimizar la transferencia de datos o quitar las transformaciones de datos costosos
- Habilitar pruebas automatizadas y reciclaje de modelos

Dado que la elección de técnicas de optimización depende de la tarea que es crítica para la aplicación o el caso de uso, los casos prácticos cubrir tanto sugerencias generales de rendimiento e instrucciones sobre cómo optimizar un escenario concreto, la optimización de puntuación por lotes.

+ **Opciones de optimización individual en SQL Server**

    En el primer caso práctico de rendimiento, varias pruebas se ejecutaron en un único conjunto de datos mediante un único tipo de modelo. El algoritmo rxLinMod en RevoscaleR se usó para crear un modelo y crear puntuaciones a partir de él, pero el código, así como las tablas de datos subyacentes se modificaron sistemáticamente para probar el impacto de cada cambio.

    Por ejemplo, en una serie de pruebas, el código de R se modificó para que se pudo establecer una comparación entre el diseño de características con una función de transformación frente a calcular previamente las características y, a continuación, cargar las características de una tabla. En otra serie de pruebas, se comparó el rendimiento de entrenamiento del modelo entre el uso de una tabla con índice estándar frente a datos en una tabla con distintos tipos de compresión o nuevos tipos de índice.

+ **Optimización para un escenario concreto de puntuación de gran volumen**

    La tarea de aprendizaje automático en el segundo caso práctico implica el procesamiento de currículos muchos enviado para varios puestos y encontrar a los mejores candidatos para cada puesto de trabajo. El propio modelo de aprendizaje automático se formula como un problema de clasificación binaria: toma una descripción resume y trabajo como entrada y genera la probabilidad de cada par resume-job. Dado que el objetivo es encontrar la mejor coincidencia, se usa un umbral de probabilidad definidas por el usuario para filtrar aún más y obtener a las concordancias de buena.

    Para esta solución, el principal objetivo era obtener una baja latencia durante la puntuación. Sin embargo, esta tarea es costosa, incluso durante el proceso de puntuación, porque cada nuevo trabajo debe coincidir con millones de currículos dentro de un período de tiempo razonable. Además, el paso de ingeniería de características produce más de 2000 funciones por trabajo o reanudar y es un cuello de botella de rendimiento significativas.

Se recomienda que revise todos los resultados desde el primer caso práctico para determinar qué técnicas son aplicables a la solución y sopesar su impacto potencial.

A continuación, revise los resultados de la puntuación de optimización caso práctico para ver cómo el autor aplica técnicas diferentes y optimizado para el servidor para admitir una carga de trabajo determinado.

## <a name="performance-optimization-process"></a>Proceso de optimización del rendimiento

Configuración y ajuste del rendimiento requiere la creación de una base sólida, en el que las optimizaciones de capa diseñadas para cargas de trabajo específicas:

- Elija un servidor apropiado para el análisis de host. Normalmente, un informe secundario, almacenamiento de datos u otro servidor que ya se usa en otros informes o análisis es preferido. Sin embargo, en una solución de procesamiento transaccional analítico (HTAP) híbrida, los datos operativos pueden utilizarse como entrada de R para puntuar rápida.

- Configurar la instancia de SQL Server para las operaciones del motor de base de datos de saldo y R o en los niveles adecuados de la ejecución del script de Python. Esto puede incluir el cambio de los valores predeterminados de SQL Server de memoria y uso de CPU, NUMA y configuración de afinidad de procesador y la creación de grupos de recursos.

- Optimizar el equipo del servidor para admitir un uso eficaz de scripts externos. Esto puede incluir el aumento del número de cuentas que se usan para la ejecución de scripts externos, habilitar la administración de paquetes, y relacionados con la asignación de usuarios a roles de seguridad.

- Aplicar optimizaciones específicas para el almacenamiento de datos y la transferencia en SQL Server, incluida la indexación y las estrategias de estadísticas, diseño de la consulta y la optimización de consultas y el diseño de tablas que se usan para el aprendizaje automático. También puede analizar orígenes de datos y datos de los métodos de transporte o modificar los procesos ETL para optimizar la extracción de características.

- Optimizar el modelo analítico para evitar deficiencias. El ámbito de las optimizaciones que son posibles dependen de la complejidad de su código de R y los paquetes y los datos que se utiliza. Tareas clave incluyen la eliminación de transformaciones de datos costosos o descargar datos preparación o característica ingeniería las tareas de R o Python para procesos ETL o SQL. También podría refactorizar las secuencias de comandos, eliminar instalaciones de paquetes en línea, divida el código de R en procedimientos independientes para el entrenamiento, puntuación y evaluación o simplificar el código para que funcione de forma más eficaz como un procedimiento almacenado.

## <a name="articles-in-this-series"></a>Artículos de esta serie

+ [Optimización del rendimiento de R en SQL Server: hardware](../r/sql-server-configuration-r-services.md)

    Proporciona instrucciones para configurar el hardware que [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] está instalado en y para configurar la instancia de SQL Server para admitir mejor los scripts externos. Resulta especialmente útil para **los administradores de base de datos**.

+ [Optimización del rendimiento de R en SQL Server - código y datos de optimización](../r/r-and-data-optimization-r-services.md)

    Proporciona sugerencias específicas sobre cómo optimizar la secuencia de comandos externo para evitar problemas conocidos. Es muy útil para **científicos de datos**.

    > [!NOTE]
    > Aunque gran parte de la información de esta sección se aplica a R en general, algunos información es específica para las funciones analíticas de RevoScaleR. Guía de rendimiento detallado no está disponible para **revoscalepy** y otros admitidos de bibliotecas de Python.
    >

+ [Optimización del rendimiento de R en SQL Server: métodos y los resultados](../r/performance-case-study-r-services.md)

    Resume los datos que se usó los dos casos prácticos, cómo se ha probado el rendimiento y cómo las optimizaciones afectan los resultados.
