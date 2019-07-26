---
title: Funcionamiento del código R mediante procedimientos almacenados
description: Inserte el código de lenguaje R en un SQL Server procedimiento almacenado para que esté disponible para cualquier aplicación cliente que tenga acceso a una base de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1ac89b23d9b027c8f5fd02daa28a4246cddf48f1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470132"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Funcionamiento del código R con procedimientos almacenados en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Al usar las características de R y Python en SQL Server Machine Learning Services, el enfoque más común para mover soluciones a un entorno de producción es mediante la inserción de código en procedimientos almacenados. En este artículo se resumen los puntos clave que debe tener en cuenta el desarrollador de SQL al operar código R mediante SQL Server.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Implementar scripts listos para producción mediante T-SQL y procedimientos almacenados

Tradicionalmente, la integración de soluciones de ciencia de datos ha diseñado una recodificación exhaustiva para admitir el rendimiento y la integración. SQL Server Machine Learning Services simplifica esta tarea, ya que el código de R y Python puede ejecutarse en SQL Server y llamarse mediante procedimientos almacenados. Para obtener más información sobre los mecanismos para insertar código en procedimientos almacenados, vea:

+ [Inicio rápido: Script R "Hello World" en SQL Server](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

En [el tutorial se puede encontrar un ejemplo más completo de la implementación de código R en producción mediante procedimientos almacenados: Análisis de datos de R para desarrolladores de SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Directrices para optimizar el código de R para SQl

Convertir el código de R en SQL es más fácil si algunas optimizaciones se realizan con antelación en el código de R o Python. Esto incluye evitar tipos de datos que causan problemas, evitar conversiones de datos innecesarias y volver a escribir el código de R como una única llamada de función que se puede parametrizar fácilmente. Para obtener más información, vea:

+ [Bibliotecas de R y tipos de datos](r-libraries-and-data-types.md)
+ [Convertir código de R para usarlo en R Services](converting-r-code-for-use-in-sql-server.md)
+ [Uso de funciones auxiliares de sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integración de R y Python con las aplicaciones

Dado que puede ejecutar R o Python desde un procedimiento almacenado, puede ejecutar scripts desde cualquier aplicación que pueda enviar una instrucción T-SQL y administrar los resultados. Por ejemplo, podría volver a entrenar un modelo según una programación mediante la [tarea ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) en Integration Services o mediante otro programador de trabajos que pueda ejecutar un procedimiento almacenado.

La puntuación es una tarea importante que se puede automatizar fácilmente o iniciar desde aplicaciones externas. Entrenar el modelo de antemano, mediante R o Python o un procedimiento almacenado, y [guardar el modelo en formato binario](../tutorials/walkthrough-build-and-save-the-model.md) en una tabla. A continuación, el modelo se puede cargar en una variable como parte de una llamada a un procedimiento almacenado, usando una de estas opciones para la puntuación de T-SQL:

+ Puntuación en [tiempo real](../real-time-scoring.md) , optimizada para lotes pequeños
+ Puntuación de fila única, para llamar desde una aplicación
+ [Puntuación nativa](../sql-native-scoring.md), para predicción rápida por lotes desde SQL Server sin llamar a R

En este tutorial se proporcionan ejemplos de puntuación mediante un procedimiento almacenado en los modos de lote y de fila única:

+ [Tutorial de ciencia de datos de un extremo a otro para R en SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vea estas plantillas de soluciones para obtener ejemplos de cómo integrar la puntuación en una aplicación:

+ [Previsión comercial](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detección de fraude](https://github.com/Microsoft/r-server-fraud-detection)
+ [Agrupación en clústeres del cliente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Impulsar el rendimiento y la escala

Aunque el lenguaje R de código abierto tiene limitaciones conocidas con respecto a grandes conjuntos de datos, las [API de paquetes de RevoScaleR](ref-r-revoscaler.md) incluidas con SQL Server servicio machine learning pueden funcionar en grandes conjuntos de datos y beneficiarse del multiproceso y de varios núcleos. cálculos de varios procesos en la base de datos.

Si la solución de R usa agregaciones complejas o implica grandes conjuntos de usuarios, puede aprovechar las agregaciones en memoria y los índices de almacén de columnas muy eficaces de SQL Server y permitir que el código de R controle los cálculos estadísticos y la puntuación.

Para obtener más información acerca de cómo mejorar el rendimiento en SQL Server Machine Learning, consulte:

+ [Optimización del rendimiento para SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Sugerencias y trucos para la optimización del rendimiento](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adaptación del código R para otras plataformas o contextos de cálculo

El mismo código de R que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con datos se puede usar en otros orígenes de datos, como Spark en HDFS, cuando se usa la [opción de servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) en SQL Server instalación o cuando se instala el producto de la marca que no es de SQL, Microsoft machine learning Servidor (anteriormente conocido como **Microsoft R Server**):

+ [Machine Learning Server documentación](https://docs.microsoft.com/r-server/)

+ [Explorar R a RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Escribir algoritmos de fragmentación](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Computación con macrodatos en R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desarrolle su propio algoritmo paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

