---
title: Aplicar el código de R en SQL Server Machine Learning Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 41da5cfe2e545bdcbc59f8d557afc599177c9d5e
ms.sourcegitcommit: f083867f97bb740caa211ca37cb046641172b8c0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38952468"
---
# <a name="operationalize-r-code-machine-learning-services"></a>Aplicar el código de R (Machine Learning Services)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. El desarrollador de la base de datos funciona con los desarrolladores de aplicaciones, los desarrolladores de SQL y científicos de datos para diseñar e implementar soluciones.

En este artículo se resume los puntos clave para el desarrollador de la base de datos que debe considerar al código de R con SQL Server de puesta en marcha.

## <a name="get-started-with-r-code-in-sql-server"></a>Empezar a trabajar con código de R en SQL Server

Tradicionalmente, la integración de soluciones de aprendizaje automático ha pensado recodificar extenso para admitir rendimiento y la integración. Sin embargo, procedimientos almacenados mover código de R y Python en un entorno de producción es mucho más fácil en SQL Server Machine Learning Services, ya que el código se puede ejecutar en SQL Server y se las llama usando. Puede seguir usando herramientas conocidas y no es necesario instalar un entorno de desarrollo de R. 

Para obtener más información sobre la sintaxis básica, consulte:

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [Uso de código de R en SQL](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para obtener un ejemplo de cómo puede implementar código R en producción mediante el uso de procedimientos almacenados, vea:

+ [En análisis base de datos para desarrolladores de SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="optimize-your-r-code"></a>Optimizar el código de R

Por supuesto, convertir el código de R en SQL es más fácil si algunas optimizaciones se realizan con antelación en el código de R o Python. Se trata de evitar los tipos de datos que producen problemas, evitar las conversiones de datos innecesarios y volver a escribir el código de R como una única llamada de función que se puede parametrizar fácilmente. Para obtener más información, vea:

+ [Bibliotecas de R y tipos de datos](r-libraries-and-data-types.md)

+ [Convertir código de R para usarlo en R Services](converting-r-code-for-use-in-sql-server.md)

+ [Generar una R procedimiento almacenado mediante sqlrutils](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>Integración de R y Python con aplicaciones

Machine Learning Services se pueden iniciar desde un procedimiento almacenado, puede ejecutar scripts de R o Python desde cualquier aplicación que pueda enviar una instrucción de Transact-SQL y controlar los resultados.

Por ejemplo, podría volver a entrenar un modelo según una programación mediante el uso de la tarea Ejecutar T-SQL en Integration Services, o mediante otro programador de trabajos que se puede ejecutar un procedimiento almacenado.

La puntuación es una tarea importante que fácilmente se puede automatizar o iniciar desde aplicaciones externas. Entrenar el modelo de antemano, mediante R o Python o un procedimiento almacenado y guardar el modelo en formato binario en una tabla. A continuación, se puede cargar el modelo en una variable como parte de una llamada de procedimiento almacenado, mediante una de estas opciones para la puntuación de T-SQL:

+ [En tiempo real](../real-time-scoring.md) puntuación, optimizado para los lotes pequeños
+ Fila única de puntuación, para llamar desde una aplicación
+ [Puntuación nativa](../sql-native-scoring.md), para la predicción de batch rápidas de SQL Server sin llamar a R

En este tutorial se proporciona ejemplos de puntuación mediante un procedimiento almacenado en el lote y modos de fila única:

+ [Extremo a otro tutorial de ciencia de datos de R en SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Consulte estas plantillas de solución para obtener ejemplos de cómo integrar una aplicación de puntuación:

+ [Previsión de ventas](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detección de fraudes](https://github.com/Microsoft/r-server-fraud-detection)
+ [Agrupación en clústeres de cliente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Mejorar el rendimiento y escalabilidad

Aunque el lenguaje R de código abierto se sabe que tienen limitaciones, el paquete RevoScaleR API pueden operar en conjuntos de datos grandes y aprovechar los cálculos en bases de datos de varios subprocesos, de varios núcleos, varios procesos de.

Si la solución R usa agregaciones complejas o implica grandes conjuntos de datos, puede aprovechar los índices de almacén de columnas y altamente eficientes agregaciones en memoria de SQL Server y permitir que el código R controle los cálculos estadísticos y de puntuación.

Para obtener más información acerca de cómo mejorar el rendimiento de SQL Server Machine Learning, consulte:

+ [Optimización del rendimiento de SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Trucos y sugerencias de optimización de rendimiento](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adapta el código de R para otras plataformas o contextos de cálculo

El mismo código de R que se ejecuta con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos se pueden usar con otros orígenes de datos, como Hadoop y en otros contextos de cálculo.

Para obtener más información acerca de las plataformas compatibles con Microsoft R, consulte:

+ [Introducción a Microsoft R](https://docs.microsoft.com/r-server/)

+ [Explorar RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

Para obtener más información acerca de cómo puede optimizar las soluciones de Microsoft R para ejecutarse en varias plataformas o de datos de gran tamaño, consulte:

+ [Escribir algoritmos de fragmentación](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Informática con big data en R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desarrollar su propio algoritmo en paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

