---
title: Optimización del rendimiento de R
description: En este artículo se describe la optimización del rendimiento de R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 991f9f0ddbe58e5591a89ff16bf8455d5a5cdca4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756474"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Optimización del rendimiento de R en SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artículo es el primero de una serie de cuatro artículos que describen la optimización del rendimiento de R Services, en función de dos casos prácticos:

- Pruebas de rendimiento realizadas por el equipo de desarrollo del producto para validar el perfil de rendimiento de las soluciones de R.

- Optimización del rendimiento por parte del equipo de ciencia de datos de Microsoft para un escenario específico de aprendizaje automático solicitado a menudo por los clientes.

El objetivo de esta serie es proporcionar instrucciones sobre los tipos de técnicas de optimización del rendimiento que son más útiles para ejecutar trabajos de R en SQL Server.

+ En este (primer) tema se ofrece información general sobre la arquitectura y algunos problemas comunes que se observan al optimizar las tareas de ciencia de datos.
+ En el segundo artículo se tratan las optimizaciones específicas de hardware y SQL Server.
+ En el tercer artículo se tratan las optimizaciones del código de R y los recursos de operacionalización.
+ En el cuarto artículo se describen los métodos de prueba en detalle y se notifican los resultados y las conclusiones.

**Se aplica a:** SQL Server 2016 R Services y SQL Server Machine Learning Services

## <a name="performance-goals-and-targeted-scenarios"></a>Objetivos de rendimiento y escenarios de destino

La característica R Services se presentó en SQL Server 2016 para admitir la ejecución de scripts de R mediante SQL Server. Cuando se usa esta característica, el runtime de R funciona en un proceso independiente del motor de base de datos, pero intercambia los datos de forma segura con este motor, mediante recursos del servidor y servicios que interactúan con SQL Server, como Trusted Launchpad.

En SQL Server 2017, se anunció compatibilidad con la ejecución de scripts de Python con la misma arquitectura, con un lenguaje adicional que seguir en el futuro.

A medida que crece el número de versiones e idiomas compatibles, es importante que el administrador de la base de datos y el arquitecto de la base de datos conozcan el potencial de contención de recursos debido a trabajos de aprendizaje automático, y que puedan configurar el servidor para que admita las nuevas cargas de trabajo. Aunque mantener el análisis cerca de los datos elimina movimientos de datos inseguros, también desplaza las cargas de trabajo analíticas del portátil del científico de datos al servidor que hospeda los datos.

La optimización del rendimiento del aprendizaje automático no es claramente una propuesta única. Es posible que las siguientes tareas comunes tengan perfiles de rendimiento muy diferentes:

- Tareas de entrenamiento: creación y entrenamiento de un modelo de regresión frente a entrenamiento de una red neuronal
- Ingeniería de características con R frente a extracción de características con T-SQL
- Puntuación en filas individuales o lotes pequeños frente a puntuación masiva con entradas tabulares
- Ejecución de la puntuación en R frente a la implementación de modelos en producción en SQL Server en procedimientos almacenados
- Modificación del código de R para minimizar la transferencia de datos o quitar costosas transformaciones de datos
- Habilitación de pruebas automatizadas y nuevo entrenamiento de modelos

Dado que la elección de las técnicas de optimización depende de la tarea que sea crítica para su aplicación o caso de uso, los casos prácticos cubren sugerencias de rendimiento generales e instrucciones sobre cómo optimizar para un escenario concreto, la optimización de la puntuación por lotes.

+ **Opciones de optimización individuales en SQL Server**

    En el primer caso práctico de rendimiento, se han ejecutado varias pruebas en un solo conjunto de datos con un solo tipo de modelo. Se ha usado el algoritmo rxLinMod de RevoscaleR para compilar un modelo y crear puntuaciones a partir de él, pero el código, así como las tablas de datos subyacentes, se han modificado sistemáticamente para probar el impacto de cada cambio.

    Por ejemplo, en una serie de pruebas, se ha modificado el código de R para poder realizar una comparación entre la ingeniería de características con una función de transformación frente al cálculo previo de las características y la posterior carga de características desde una tabla. En otra serie de pruebas, se ha comparado el rendimiento de entrenamiento del modelo entre el uso de una tabla indexada estándar frente a los datos de una tabla con diversos tipos de compresión o nuevos tipos de índice.

+ **Optimización para un escenario específico de puntuaciones de gran volumen**

    La tarea de aprendizaje automático del segundo caso práctico implica el procesamiento de muchos currículos enviados para varios puestos y la búsqueda del mejor candidato para cada puesto de trabajo. El propio modelo de aprendizaje automático se formula como un problema de clasificación binaria: toma un currículo y la descripción del trabajo como entrada y genera la probabilidad de cada par currículo-trabajo. Dado que el objetivo es encontrar la mejor coincidencia, se usa un umbral de probabilidad definido por el usuario para filtrar y obtener solo las coincidencias válidas.

    Para esta solución, el objetivo principal era lograr una baja latencia durante la puntuación. Si bien, esta tarea es costosa desde el punto de vista del proceso incluso durante el proceso de puntuación, ya que cada nuevo trabajo debe compararse con millones de currículos en un plazo de tiempo razonable. Además, el paso de ingeniería de características produce más de 2000 características por currículo o trabajo, y supone un importante cuello de botella en el rendimiento.

Se recomienda que revise todos los resultados del primer caso práctico para determinar las técnicas que se aplican a la solución y sopese su impacto potencial.

Después, revise los resultados del caso práctico de optimización de puntuación para ver cómo el autor ha aplicado distintas técnicas y ha optimizado el servidor para admitir una carga de trabajo determinada.

## <a name="performance-optimization-process"></a>Proceso de optimización del rendimiento

La configuración y la optimización del rendimiento requieren la creación de una base sólida, sobre la que se puedan realizar optimizaciones en capas diseñadas para cargas de trabajo específicas:

- Elija un servidor adecuado para hospedar análisis. Por lo general, se prefiere un servidor secundario de generación de informes, un almacén de datos u otro servidor que ya se utilice para otros tipos de generación de informes o análisis. En cambio, en una solución híbrida de procesamiento analítico de transacciones (HTAP), los datos operativos se pueden usar como entrada de R para una puntuación rápida.

- Configure la instancia de SQL Server para equilibrar las operaciones del motor de base de datos y la ejecución de scripts de R o Python en los niveles adecuados. Esto puede incluir el cambio de valores predeterminados de SQL Server sobre el uso de CPU y de memoria, la configuración de afinidad del procesador y de NUMA, y la creación de grupos de recursos.

- Optimice el equipo servidor para admitir el uso eficaz de scripts externos. Esto puede incluir el aumento del número de cuentas usadas para la ejecución de scripts externos, la habilitación de la administración de paquetes y la asignación de usuarios a roles de seguridad relacionados.

- La aplicación de optimizaciones específicas para el almacenamiento de datos y la transferencia en SQL Server, incluidas las estrategias de indexación y estadísticas, el diseño de consultas y la optimización de consultas, además del diseño de las tablas que se usan para el aprendizaje automático. También puede analizar los orígenes de datos y los métodos de transporte de datos, o modificar los procesos ETL para optimizar la extracción de características.

- Ajuste el modelo analítico para evitar ineficiencias. El ámbito de las optimizaciones que son posibles depende de la complejidad del código de R y de los paquetes y datos que se usan. Entre las tareas clave se incluyen la eliminación de costosas transformaciones de datos o la descarga de tareas de preparación de datos o de ingeniería de características desde R o Python hasta procesos ETL o SQL. También puede refactorizar scripts, eliminar instalaciones de paquetes en línea, dividir código de R en procedimientos independientes de entrenamiento, puntuación y evaluación, o simplificar el código para que funcione de forma más eficaz como procedimiento almacenado.

## <a name="articles-in-this-series"></a>Artículos de esta serie

+ [Optimización del rendimiento de R en SQL Server: hardware](../r/sql-server-configuration-r-services.md)

    Proporciona instrucciones para configurar el hardware en el que está instalado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y para configurar la instancia de SQL Server con el fin de mejorar la compatibilidad con scripts externos. Resulta especialmente útil para los **administradores de bases de datos**.

+ [Optimización del rendimiento de R en SQL Server: optimización de datos y de código](../r/r-and-data-optimization-r-services.md)

    Ofrece sugerencias específicas sobre cómo optimizar el script externo para evitar problemas conocidos. Resulta muy útil para **científicos de datos**.

    > [!NOTE]
    > Aunque la mayor parte de la información de esta sección se aplica a R en general, cierta información es específica de las funciones analíticas de RevoScaleR. La guía de rendimiento detallada no está disponible para **revoscalepy** y otras bibliotecas de Python compatibles.
    >

+ [Optimización del rendimiento de R en SQL Server: métodos y resultados](../r/performance-case-study-r-services.md)

    Resume los datos que se han usado en los dos casos prácticos, cómo se ha probado el rendimiento y cómo han incidido las optimizaciones en los resultados.
