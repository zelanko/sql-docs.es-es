---
title: Implementación de código de R en procedimientos almacenados
description: Inserte código de lenguaje R en un procedimiento almacenado de SQL Server para que esté disponible para cualquier aplicación cliente que tenga acceso a una base de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/15/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9790f5a5d82584bb0d09fda92c1a7048d384e119
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242331"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Operacionalización de código de R con procedimientos almacenados en SQL Server Machine Learning Services
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Al usar las características de R y Python en SQL Server Machine Learning Services, el enfoque más común para trasladar soluciones a un entorno de producción es insertar código en procedimientos almacenados. En este artículo se resumen los puntos clave que debe tener en cuenta el desarrollador de SQL al operacionalizar código de R mediante SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Implementación de scripts listos para producción mediante T-SQL y procedimientos almacenados

Tradicionalmente, la integración de soluciones de ciencia de datos ha implicado volver a codificar de forma exhaustiva para admitir el rendimiento y la integración. SQL Server Machine Learning Services simplifica esta tarea, ya que el código de R y Python puede ejecutarse en SQL Server y llamarse mediante procedimientos almacenados. Para más información sobre los mecanismos para insertar código en procedimientos almacenados, vea:

+ [Creación y ejecución de scripts de R sencillos en SQL Server](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Puede encontrar un ejemplo más completo de la implementación de código de R en producción mediante procedimientos almacenados en [Tutorial: Análisis de datos de R para desarrolladores de SQL](../../machine-learning/tutorials/sqldev-in-database-r-for-sql-developers.md).

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Instrucciones para optimizar código de R para SQL

Convertir el código de R en SQL es más fácil si se llevan a cabo algunas optimizaciones con antelación en el código de R o Python. Esto incluye evitar tipos de datos que causan problemas, evitar conversiones de datos innecesarias y volver a escribir el código de R como una única llamada de función que se pueda parametrizar fácilmente. Para más información, consulte:

+ [Bibliotecas de R y tipos de datos](r-libraries-and-data-types.md)
+ [Convertir código de R para usarlo en R Services](converting-r-code-for-use-in-sql-server.md)
+ [Uso de funciones auxiliares de sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integración de R y Python con aplicaciones

Dado que puede ejecutar R o Python desde un procedimiento almacenado, se pueden ejecutar scripts desde cualquier aplicación que pueda enviar una instrucción T-SQL y controlar los resultados. Por ejemplo, podría volver a entrenar un modelo según una programación mediante la [tarea Ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) de Integration Services o mediante otro programador de trabajos que pueda ejecutar un procedimiento almacenado.

La puntuación es una tarea importante que se puede automatizar fácilmente o iniciar desde aplicaciones externas. Entrene el modelo con antelación, mediante R, Python o un procedimiento almacenado, y [guarde el modelo en formato binario](../tutorials/walkthrough-build-and-save-the-model.md) en una tabla. Después, el modelo se puede cargar en una variable como parte de una llamada a un procedimiento almacenado, mediante una de estas opciones para la puntuación de T-SQL:

+ Puntuación en tiempo real, optimizada para lotes pequeños.
+ Puntuación de fila única, para llamar desde una aplicación.
+ [Puntuación nativa](../predictions/native-scoring-predict-transact-sql.md), para una predicción rápida de lotes de SQL Server sin llamar a R.

En este tutorial se proporcionan ejemplos de puntuación mediante un procedimiento almacenado en los modos de lotes y de fila única:

+ [Tutorial de ciencia de datos de un extremo a otro para R en SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vea estas plantillas de soluciones para consultar ejemplos de cómo integrar la puntuación en una aplicación:

+ [Previsión de comercio minorista](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/README.md)
+ [Detección de fraude](https://github.com/Microsoft/r-server-fraud-detection)
+ [Agrupación en clústeres de clientes](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Aumento del rendimiento y la escalabilidad

Aunque se sabe que el lenguaje R de código abierto presenta limitaciones con respecto a conjuntos de datos de gran tamaño, las [API del paquete RevoScaleR](ref-r-revoscaler.md) que se incluyen con SQL Server Machine Learning Service pueden funcionar en conjuntos de datos de gran tamaño y aprovechar los cálculos de varios procesos, núcleos y procesos en la base de datos.

Si la solución de R usa agregaciones complejas o implica conjuntos de datos de gran tamaño, puede aprovechar los índices de almacén de columnas y las agregaciones en memoria altamente eficaces de SQL Server y permitir que el código de R controle la puntuación y los cálculos estadísticos.

Para más información sobre cómo mejorar el rendimiento en SQL Server Machine Learning, vea:

+ [Optimización del rendimiento de SQL Server R Services](../../machine-learning/r/sql-server-r-services-performance-tuning.md)
+ [Sugerencias y trucos para la optimización del rendimiento](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptación del código de R para otras plataformas o contextos de cálculo

El mismo código de R que se ejecuta en datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede usar en otros orígenes de datos, como Spark en HDFS, al usar la [opción de servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) en la configuración de SQL Server o al instalar el producto que no es de SQL Microsoft Machine Learning Server (anteriormente conocido como **Microsoft R Server**):

+ [Documentación de Machine Learning Server](https://docs.microsoft.com/r-server/)

+ [Exploración de R a RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Escritura de algoritmos de fragmentación](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Computación con macrodatos en R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desarrollo de su propio algoritmo paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

