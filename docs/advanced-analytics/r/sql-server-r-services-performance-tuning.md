---
title: Optimización del rendimiento de SQL Server R Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 974e4ab2a33e7cc218c22246f7279a131893f119
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203127"
---
# <a name="performance-tuning-for-r-in-sql-server"></a>Ajuste del rendimiento de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo es el primer elemento de una serie de cuatro artículos que describen la optimización de rendimiento para servicios de R, basados en dos casos prácticos:

- Pruebas de rendimiento realizadas por el equipo de desarrollo del producto para validar el perfil de rendimiento de soluciones en R

- Optimización del rendimiento por el equipo de ciencia de datos de Microsoft para un escenario de aprendizaje automático específico a menudo solicitado por los clientes.

El objetivo de esta serie es ofrecer orientación sobre los tipos de técnicas que son muy útiles para ejecutar trabajos de R en SQL Server para la optimización de rendimiento.

+ En este tema (primera) proporciona una visión general de la arquitectura y algunos problemas comunes al optimizar para tareas de ciencia de datos.
+ El segundo artículo trata las optimizaciones de SQL Server y de hardware específicas.
+ Tercer este artículo describen las optimizaciones en el código de R y recursos para la puesta en marcha.
+ El cuarto artículo describen los métodos de prueba en detalle y los resultados de informes y conclusiones.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="performance-goals-and-targeted-scenarios"></a>Objetivos de rendimiento y escenarios concretos

La característica Servicios de R se introdujo en SQL Server 2016 para admitir la ejecución de scripts de R mediante SQL Server. Si usa esta característica, el runtime de R funciona en un proceso independiente desde el motor de base de datos, pero intercambia datos de forma segura con el motor de base de datos, el uso de recursos de servidor y servicios que interactúan con SQL Server, como el Launchpad de confianza.

En SQL Server 2017, soporte técnico se anunció para ejecutar scripts de Python con la misma arquitectura de idioma adicionales para seguir en el futuro.

A medida que aumenta el número de versiones admitidas y el idioma, es importante que el Administrador de base de datos y el arquitecto de base de datos son conscientes de la posibilidad de contención de recursos debido a trabajos de aprendizaje de máquina, y que se les permite configurar el servidor para admitir las cargas de trabajo nuevo. Aunque mantener análisis cerca de los datos, elimina movimientos de datos no seguro, también se desplaza las cargas de trabajo analíticos desactivar el equipo portátil de los científicos de datos y en el servidor que hospeda los datos.

Optimización del rendimiento para el aprendizaje automático no es claramente una propuesta única. Las siguientes tareas comunes podrían tener perfiles de rendimiento muy diferentes:

- Tareas de entrenamiento: crear y entrenar un modelo de regresión frente a una red neuronal de entrenamiento
- Uso de R frente a la extracción de características mediante T-SQL de ingeniería de característica
- La puntuación en filas individuales y de lotes pequeños, frente a masiva utilizando entradas tabulares de puntuación
- Ejecución de R de puntuación frente a la implementación de modelos en producción en SQL Server en los procedimientos almacenados
- Modificar el código de R para minimizar la transferencia de datos o quitar las transformaciones de datos costosos
- Habilitar pruebas automatizadas y reciclaje de modelos

Dado que la elección de técnicas de optimización depende de la tarea que es crítica para la aplicación o el caso de uso, los casos de estudio abarcan tanto sugerencias generales de rendimiento e instrucciones sobre cómo optimizar para un escenario concreto, la optimización de la puntuación del lote.

+ **Opciones de optimización individuales en SQL Server**

    En el primer rendimiento caso práctico, varias pruebas se ejecutaron en un único conjunto de datos utilizando un tipo de modelo. El algoritmo rxLinMod en RevoscaleR se usó para crear un modelo y crear puntuaciones a partir de él, pero el código, así como las tablas de datos subyacentes se modificaron sistemáticamente para probar el impacto de cada cambio.

    Por ejemplo, en una ejecución de pruebas, el código de R se modificó para que una comparación podría estar entre ingeniería de característica con una función de transformación frente a calcular previamente las características y, a continuación, cargar características de una tabla. En otra ejecución de prueba, el rendimiento de entrenamiento del modelo se comparó entre el uso de una tabla con índice estándar frente a datos en una tabla con distintos tipos de compresión o nuevos tipos de índice.

+ **Optimización para un escenario concreto de puntuación de gran volumen**

    Las tareas de aprendizaje automático en el segundo caso práctico implica el procesamiento de currículos muchos enviado para varias posiciones y buscar a los mejores candidatos para cada puesto de trabajo. El propio modelo de aprendizaje automático se formula como un problema de clasificación binaria: tiene una descripción resume y trabajo como entrada y se genera la probabilidad de cada par resume-job. Dado que el objetivo es encontrar la mejor coincidencia, un umbral de probabilidad definidas por el usuario se utiliza para filtrar aún más y obtener a solo las coincidencias buena.

    Para esta solución, el principal objetivo era lograr una latencia baja durante la puntuación. Sin embargo, esta tarea es cara incluso durante el proceso de puntuación, porque cada nuevo trabajo debe coincidir en millones de currículos dentro de un período de tiempo razonable. Además, el paso de ingeniería de características genera más de 2000 características por reanudar o trabajo y es un cuello de botella de rendimiento significativas.

Se recomienda que revise todos los resultados desde el primer caso práctico para determinar qué técnicas son aplicables a la solución y peso es su impacto potencial.

A continuación, revise los resultados de la puntuación de optimización caso práctico para ver cómo el autor aplica técnicas diferentes y con optimización para el servidor para admitir una carga de trabajo determinado.

## <a name="performance-optimization-process"></a>Proceso de optimización de rendimiento

Configuración y optimización del rendimiento requiere la creación de una base sólida, en el que las optimizaciones de capa diseñadas para cargas de trabajo específicas:

- Elija un servidor apropiado para el análisis de host. Normalmente, un informe secundario, almacenamiento de datos u otro servidor que ya se usa para otros informes o análisis es preferido. Sin embargo, en una solución de procesamiento transaccional analítico (HTAP) híbrida, los datos operativos pueden utilizarse como entrada de R para puntuar rápida.

- Configurar la instancia de SQL Server para las operaciones del motor de base de datos de equilibrio y R o en los niveles adecuados de la ejecución del script de Python. Esto puede incluir cambiar valores predeterminados de SQL Server para la memoria y uso de CPU, NUMA y configuración de la afinidad de procesador y creación de grupos de recursos.

- Optimizar el equipo del servidor para admitir un uso eficaz de scripts externos. Esto puede incluir el aumento del número de cuentas que se usan para la ejecución de scripts externos, habilitar la administración de paquetes, y relacionados con la asignación de usuarios a roles de seguridad.

- Aplicar las optimizaciones específicas para el almacenamiento de datos y la transferencia en SQL Server, incluida la indización y las estrategias de estadísticas, diseño de la consulta y optimización de consultas y el diseño de tablas que se usan para el aprendizaje automático. También puede analizar los orígenes de datos y datos de métodos de transporte, o modificar los procesos ETL para optimizar la extracción de características.

- Optimizar el modelo analítico para evitar las ineficiencias. El ámbito de las optimizaciones que son posibles dependen de la complejidad de su código en R y los paquetes y los datos que se utiliza. Tareas clave incluyen lo que elimina las transformaciones de datos costosas o descargar datos preparación o característica ingeniería las tareas de R o Python para procesos ETL o SQL. También podría refactorizar las secuencias de comandos, eliminar la instalación de paquete en línea, dividir código R en procedimientos independientes para el entrenamiento, la puntuación y evaluación o simplificar el código para que funcione de forma más eficaz que un procedimiento almacenado.

## <a name="articles-in-this-series"></a>Artículos de esta serie

+ [Ajuste del rendimiento de R en SQL Server - hardware](..\r\sql-server-configuration-r-services.md)

    Proporciona instrucciones para configurar el hardware que [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] está instalado en y para configurar la instancia de SQL Server para admitir mejor scripts externos. Es especialmente útil para **los administradores de base de datos**.

+ [Ajuste del rendimiento de R en SQL Server: código y datos de optimización](..\r\r-and-data-optimization-r-services.md)

    Proporciona sugerencias específicas sobre cómo optimizar la secuencia de comandos externo para evitar los problemas conocidos. Es muy útil para **científicos de datos**.

    [!NOTE]
    > Aunque gran parte de la información de esta sección se aplica a R en general, parte de la información es específico de funciones analíticas RevoScaleR. Guía de rendimiento detallado no está disponible para **revoscalepy** y otros admiten bibliotecas de Python.

+ [Ajuste del rendimiento de R en SQL Server: métodos y resultados](..\r\performance-case-study-r-services.md)

    Resume los datos que se usó los dos casos prácticos, cómo se prueba el rendimiento y cómo afectan las optimizaciones de los resultados.
