---
title: "Introducción a SQL Server de aprendizaje automático | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 12/07/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: d643bbdf32b946c5342484fa531303b5b74f4bcb
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="getting-started-with-sql-server-machine-learning"></a>Introducción a SQL Server de aprendizaje automático
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Servicios de aprendizaje de máquina en SQL Server está diseñado para admitir tareas de ciencia de datos sin exponer los datos a riesgos de seguridad o móvil unnecesarily de datos.

+ En SQL Server 2016, puede trabajar con las herramientas de R, pero escalar su análisis a miles de millones de registros al tiempo que aumenta el rendimiento. Integración de aprendizaje automático con SQL Server también significa que se puede colocar el código de R en producción sin tener que volver a codificar.

+ SQL Server 2017 agrega compatibilidad para código de Python, con el mismo marco de extensibilidad.

En este tema se describe los escenarios claves para el uso de R o Python en bases de datos y proporciona recursos para ayudarle a empezar a trabajar con sus propias soluciones.

Se aplica a: servicios (en bases de datos) de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

> [!NOTE]
> SQL Server 2016 incluye compatibilidad con solo el lenguaje R. Compatibilidad con lenguaje de Python requiere SQL Server 2017 CTP 2.0.

## <a name="step-1-set-up-sql-server-machine-learning-services"></a>Paso 1. Configurar servicios de aprendizaje de máquina SQL Server

1. Ejecute el programa de instalación de SQL Server e instale al menos una instancia del motor de base de datos de SQL Server.
2. Agregar la característica que admite la ejecución de tiempos de ejecución externos.
3. En SQL Server 2016, R se agrega de forma predeterminada. En SQL Server 2017, debe seleccionar un idioma que deseas agregar. Puede seleccionar R o Python o permitir.
4. Cuando se realiza el programa de instalación, realizar algunos pasos adicionales para habilitar la ejecución de scripts externos y reiniciar el servidor.

**Recursos**

+ [Configurar SQL Server con aprendizaje automático](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

> [!TIP]  
> ¿Necesita crear un servidor para trabajos de R pero no necesita SQL Server? Pruebe [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx).  

## <a name="step-2-develop-your-r-or-python-solutions"></a>Paso 2. Desarrollar la R o soluciones de Python

Los científicos de datos utilizan normalmente R o Python en su propia estación de trabajo portátil o de desarrollo, para explorar datos y generar y ajustar modelos predictivos hasta que consigue un buen modelo predictivo. 

Con servicios de aprendizaje de máquina en SQL Server, no es necesario que cambie este proceso. Una vez completada la instalación, puede ejecutar código R o Python en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tanto local como remotamente:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **Usar el IDE prefiere**. Los clientes de[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] proporcionan a los científicos de datos todas las herramientas que necesitan para experimentar y desarrollar soluciones. Estas herramientas incluyen el tiempo de ejecución de R, la biblioteca Intel Math Kernel Library para mejorar el rendimiento de las operaciones estándar de R y un conjunto de paquetes de R mejorados con los que puede ejecutarse código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

+ **Trabajar de forma local como remota**. Los científicos de datos pueden conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y mover los datos al cliente para realizar un análisis local del modo habitual. En cambio, una solución más eficaz consiste en usar las API de **ScaleR** para enviar los cálculos al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , lo que evita tener que realizar los costosos y poco seguros movimientos de datos.

+ **Incruste scripts de R o Python en [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos almacenados**. Cuando el código está totalmente optimizado, inclúyala en un procedimiento almacenado para evitar movimientos de datos innecesarios y optimizar las tareas de procesamiento de datos.


**Recursos**

+ Instalar [R Tools para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation) o RStudio.  

## <a name="step-3-optimize"></a>Paso 3. Optimización

Cuando el modelo está listo para escalar de datos empresariales, los científicos de datos a menudo funcionará con el desarrollador DBA o SQL para optimizar los procesos, como:

+ Ingeniería de características
+ Recopilación de datos y transformación de datos
+ Puntuaciones

Tradicionalmente científicos de datos con R han tenido problemas con el rendimiento y la escalabilidad, especialmente cuando se usa el conjunto de datos grande. Eso es porque la implementación en tiempo de ejecución común es de subproceso único y puede dar cabida a los conjuntos de datos que caben en la memoria disponible en el equipo local. Integración con servicios de aprendizaje de máquina de SQl Server proporciona varias características para mejorar el rendimiento, con más datos:

+ **RevoScaleR**.: paquete de R esta contiene implementaciones de algunas de las funciones de R más populares, rediseñadas para ofrecer paralelismo y escalabilidad. El paquete también incluye funciones que aumentan aún más el rendimiento y la escalabilidad mediante la inserción de cálculos al equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que, normalmente, tiene mayor memoria y potencia de cálculo.

+ **revoscalepy**. Esta biblioteca de Python, nuevo y está disponible solo en SQL Server de 2017 CTP 2.0, implementa las funciones más populares en RevoScaleR, por ejemplo, los contextos de proceso remoto y el procesamiento distribuyen de muchos algoritmos que admiten.

+ Elegir el mejor lenguaje para la tarea.  R es más adecuado para realizar cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en conjunto sobre datos, aprovechan la eficacia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para lograr un rendimiento máximo. Usar el motor de base de datos en memoria para realizar cálculos muy rápidos a través de las columnas.

**Recursos**

+ [Caso práctico de rendimiento](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R y optimización de datos](../../advanced-analytics/r/r-and-data-optimization-r-services.md)


## <a name="step-4-deploy-and-consume"></a>Paso 4. Implementar y consumir

Después de que el script de R o el modelo está listo para su uso en producción, un desarrollador de la base de datos puede incrustar el código o el modelo en un procedimiento almacenado, para que el código de R o Python guardado se puede llamar desde una aplicación. Almacenar y ejecutar código R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene muchas ventajas: puede usar la cómoda interfaz de [!INCLUDE[tsql](../../includes/tsql-md.md)] y todos los cálculos realizados en la base de datos, con lo que se evita realizar movimientos de datos innecesarios.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **Seguro y extensible**. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa una nueva arquitectura de extensibilidad que mantiene el motor de base de datos seguro y aísla las sesiones de R. También podrá controlar los usuarios que pueden ejecutar scripts de R y especificar qué bases de datos pueden acceder al código R. Puede controlar la cantidad de recursos asignados al runtime de R y, de este modo, evitar que unos cálculos masivos pongan en peligro el rendimiento general del servidor.

+ **Programación y auditoría**. Cuando se ejecutan los trabajos de script externo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede controlar y auditar los datos utilizados por los científicos de datos. También puede programar trabajos y crear flujos de trabajo que contiene scripts de R o Python externos, al igual que haría programar cualquier otro trabajo de T-SQL o procedimiento almacenado.

Para aprovechar las ventajas de las características de seguridad y administración de recursos de SQL Server, el proceso de implementación puede incluir estas tareas:

+ Convertir el código de R a una función que se puede ejecutar de forma óptima en un procedimiento almacenado
+ Configurar la seguridad y el bloqueo utilizados por una tarea determinada de paquetes
+ Habilitar el regulador de recursos

**Recursos**

+ [Regulador de recursos para R](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [Administración de paquetes de R para SQL Server](../../advanced-analytics/r/r-package-management-for-sql-server-r-services.md)

## <a name="quick-starts"></a>Guías rápidas

Lea este tutorial para entender el flujo de trabajo completa, al explorar datos para crear un modelo y su implementación en SQL Server.

+ [Tutorial integral de ciencia de datos](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Obtenga información acerca de cómo usar el paquete RevoScaleR para el análisis de escalable y de alto rendimiento.

+ [Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

Especialmente para los desarrolladores de datos--proporciona todo el código R! Obtenga información acerca de cómo incrustar R en los procedimientos almacenados de SQL para crear o entrenar modelos y obtener las predicciones de un modelo almacenado.

+ [Análisis avanzado en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Obtenga información acerca de la sintaxis de R que realiza la llamada desde un procedimiento almacenado.

+ [Uso de código de R en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

## <a name="solutions"></a>Soluciones

Para obtener más ejemplos, incluidos los sector = plantillas de solución específica, consulte [tutoriales de aprendizaje de máquina de SQL Server](../tutorials/machine-learning-services-tutorials.md).
