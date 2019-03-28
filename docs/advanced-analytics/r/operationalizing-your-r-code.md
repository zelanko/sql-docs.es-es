---
title: 'Aplicar el código de R mediante procedimientos almacenados: SQL Server Machine Learning Services'
description: Insertar código de lenguaje de R en un procedimiento almacenado de SQL Server para que esté disponible para cualquier aplicación cliente que tengan acceso a una base de datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2d00e96162b492d28f0c0ec107612023c8e15e48
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512602"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>Aplicar el código de R mediante procedimientos almacenados en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Al usar las características de R y Python en SQL Server Machine Learning Services, es el enfoque más común para mover las soluciones a un entorno de producción mediante la inserción de código en los procedimientos almacenados. En este artículo se resume los puntos clave para el desarrollador SQL tener en cuenta al código de R con SQL Server de puesta en marcha.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>Implementar el script para entornos de producción mediante Transact-SQL y procedimientos almacenados

Tradicionalmente, la integración de soluciones de ciencia de datos está pensado volver a codificar una amplia para admitir rendimiento y la integración. SQL Server Machine Learning Services simplifica esta tarea porque se puede ejecutar código R y Python en SQL Server y se llama mediante procedimientos almacenados. Para obtener más información sobre el mecanismo de inserción de código en los procedimientos almacenados, vea:

+ [Inicio rápido: Script de R "Hello world" en SQL Server](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

Encontrará un ejemplo más completo de la implementación de código de R en producción mediante el uso de procedimientos almacenados en [Tutorial: Análisis de datos de R para desarrolladores de SQL](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>Directrices para optimizar el código de R para SQl

Convertir el código de R en SQL es más fácil si algunas optimizaciones se realizan con antelación en el código de R o Python. Se trata de evitar los tipos de datos que producen problemas, evitar las conversiones de datos innecesarios y volver a escribir el código de R como una única llamada de función que se puede parametrizar fácilmente. Para obtener más información, vea:

+ [Bibliotecas de R y tipos de datos](r-libraries-and-data-types.md)
+ [Convertir código de R para usarlo en R Services](converting-r-code-for-use-in-sql-server.md)
+ [Uso de funciones auxiliares de sqlrutils](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>Integración de R y Python con aplicaciones

Dado que puede ejecutar R o Python desde un procedimiento almacenado, puede ejecutar scripts desde cualquier aplicación que pueda enviar una instrucción de Transact-SQL y controlar los resultados. Por ejemplo, se podría reciclar un modelo según una programación mediante el uso de la [tarea Ejecutar T-SQL](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) en Integration Services, o mediante otro programador de trabajos que se puede ejecutar un procedimiento almacenado.

La puntuación es una tarea importante que fácilmente se puede automatizar o iniciar desde aplicaciones externas. Entrenar el modelo con antelación, mediante R o Python o un procedimiento almacenado, y [guardar el modelo en formato binario](../tutorials/walkthrough-build-and-save-the-model.md) a una tabla. A continuación, se puede cargar el modelo en una variable como parte de una llamada de procedimiento almacenado, mediante una de estas opciones para la puntuación de T-SQL:

+ [En tiempo real](../real-time-scoring.md) puntuación, optimizado para los lotes pequeños
+ Fila única de puntuación, para llamar desde una aplicación
+ [Puntuación nativa](../sql-native-scoring.md), para la predicción de batch rápidas de SQL Server sin llamar a R

En este tutorial se proporciona ejemplos de puntuación mediante un procedimiento almacenado en el lote y modos de fila única:

+ [Extremo a otro tutorial de ciencia de datos de R en SQL Server](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Consulte estas plantillas de solución para obtener ejemplos de cómo integrar una aplicación de puntuación:

+ [Previsión de ventas](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detección de fraude](https://github.com/Microsoft/r-server-fraud-detection)
+ [Agrupación en clústeres de cliente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>Mejorar el rendimiento y escalabilidad

Aunque el lenguaje de código abierto R presenta un conocido limitaciones con respecto a grandes conjuntos de datos, el [API del paquete RevoScaleR](ref-r-revoscaler.md) incluido con el servicio de SQL Server Machine Learning puede operar en conjuntos de datos grandes y beneficiarse de multiproceso , cálculos en bases de datos de varios núcleos, varios procesos.

Si la solución R usa agregaciones complejas o implica grandes conjuntos de datos, puede aprovechar los índices de almacén de columnas y altamente eficientes agregaciones en memoria de SQL Server y permitir que el código R controle los cálculos estadísticos y de puntuación.

Para obtener más información acerca de cómo mejorar el rendimiento de SQL Server Machine Learning, consulte:

+ [Optimización del rendimiento de SQL Server R Services](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Trucos y sugerencias de optimización de rendimiento](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>Adapta el código de R para otras plataformas o contextos de cálculo

El mismo código de R que se ejecuta con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos se pueden utilizar con otros orígenes de datos, como Spark a través de HDFS, cuando se usa el [opción de servidor independiente](../install/sql-machine-learning-standalone-windows-install.md) en el programa de instalación de SQL Server o al instalar el producto de marca que no sea de SQL, Microsoft Machine Learning Server (anteriormente conocida como **Microsoft R Server**):

+ [Documentación de Machine Learning Server](https://docs.microsoft.com/r-server/)

+ [Explore R a RevoScaleR](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [Escribir algoritmos de fragmentación](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [Informática con big data en R](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [Desarrollar su propio algoritmo en paralelo](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

