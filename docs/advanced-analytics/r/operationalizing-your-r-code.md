---
title: "Incorporación de operatividad a código de R (servicios de aprendizaje de máquina) | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d858352ed7dc519dfde9f625ea24cea6a538be5b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="operationalize-r-code-machine-learning-services"></a>Incorporación de operatividad a código de R (servicios de aprendizaje de máquina)

A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. El desarrollador de la base de datos funciona con los desarrolladores de aplicaciones, los desarrolladores de SQL y científicos de datos para diseñar e implementar soluciones.

En este artículo se resume los puntos clave para el desarrollador de la base de datos que debe considerar al código de R mediante SQL Server en marcha.

## <a name="get-started-with-r-code-in-sql-server"></a>Empezar a trabajar con código de R en SQL Server

Tradicionalmente, integración de soluciones de aprendizaje de máquina objetivo es volver a codificar una amplia para admitir rendimiento y la integración. Sin embargo, procedimientos almacenados mover código R y Python para un entorno de producción es mucho más fácil en servicios de aprendizaje de máquinas de Microsoft, dado que el código se puede ejecutar en SQL Server y llama mediante. Puede seguir usando herramientas conocidas y no es necesario instalar un entorno de desarrollo de R. 

Para obtener más información acerca de la sintaxis básica, vea:

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Usar código R en SQL](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para obtener un ejemplo de cómo puede implementar código R en producción mediante procedimientos almacenados, vea:

+ [En bases de datos análisis para desarrolladores de SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="optimize-your-r-code"></a>Optimizar el código de R

Por supuesto, es más fácil si algunas optimizaciones se realizan con antelación en el código de R o Python convertir el código de R en SQL. Esto incluye evitar los tipos de datos que provocan problemas, evitar las conversiones de datos innecesarios y volver a escribir el código de R como una única llamada de función que se puede parametrizar fácilmente. Para obtener más información, vea:

+ [Tipos de datos y las bibliotecas de R](r-libraries-and-data-types.md)

+ [Convertir código de R para su uso en R Services](converting-r-code-for-use-in-sql-server.md)

+ [Generar una R procedimiento almacenado mediante sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>Integrar R y Python con aplicaciones

Servicios de aprendizaje de máquina se pueden iniciar desde un procedimiento almacenado, puede ejecutar scripts de R o Python desde cualquier aplicación que pueda enviar una instrucción de T-SQL y controlar los resultados.

Por ejemplo, puede volver a entrenar un modelo en una programación mediante la tarea Ejecutar T-SQL en Integration Services, o mediante otro programador de trabajos que se puede ejecutar un procedimiento almacenado.

La puntuación es una tarea importante que se puede fácilmente automatizada, o iniciar desde aplicaciones externas. Entrenar el modelo de antemano, mediante R, Python o un procedimiento almacenado y guardar el modelo en formato binario en una tabla. A continuación, se puede cargar el modelo en una variable como parte de una llamada de procedimiento almacenado, mediante una de estas opciones para la puntuación de T-SQL:

+ [En tiempo real](../real-time-scoring.md) de puntuación, optimizado para los lotes pequeños
+ Puntuación, para llamar desde una aplicación de varias filas
+ [Puntuación nativo](../sql-native-scoring.md), para la predicción por lotes rápidamente desde SQL Server sin llamar a R

Este tutorial proporciona ejemplos de puntuación mediante un procedimiento almacenado en el lote y modos de fila:

+ [Extremo a extremo tutorial de ciencia de datos para R en SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vea estas plantillas de solución para obtener ejemplos de cómo integrar en una aplicación de puntuación:

+ [Previsión de comercio minorista](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detección de fraudes](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [Cliente de agrupación en clústeres](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Mejorar el rendimiento y la escala

Aunque el lenguaje de código abierto R se sabe que tienen limitaciones, el paquete RevoScaleR API pueden operar en conjuntos de datos grandes y aprovechar los cálculos en bases de datos de varios subprocesos, de varios núcleos, varios procesos de.

Si la solución R usa agregaciones complejas o implica grandes conjuntos de datos, puede aprovechar altamente eficientes agregaciones en memoria e índices de almacén de columnas de SQL Server y dejar que el código R controle los cálculos estadísticos y de puntuación.

Para obtener más información acerca de cómo mejorar el rendimiento en el aprendizaje automático de SQL Server, vea:

+ [Ajuste del rendimiento para SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Sugerencias y trucos para la optimización de rendimiento](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adapta el código de R para otras plataformas o contextos de proceso

El mismo código de R que se ejecutan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos se puede utilizar con otros orígenes de datos, como Hadoop y en otros contextos de proceso.

Para obtener más información acerca de las plataformas compatibles con Microsoft R, vea:

+ [Introducción a Microsoft R](https://docs.microsoft.com/r-server/)

+ [Explorar RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

Para obtener más información acerca de cómo optimizar sus soluciones de Microsoft R para ejecutarse en datos de gran tamaño o varias plataformas, vea:

+ [Escribir algoritmos de fragmentación](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Informática con grandes cantidades de datos en R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desarrollar su propio algoritmo paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)


