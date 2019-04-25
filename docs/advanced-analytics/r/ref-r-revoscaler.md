---
title: Biblioteca de funciones de RevoScaleR R - SQL Server Machine Learning Services
description: Introducción a la biblioteca de funciones de RevoScaleR en SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3745c6cd8c340ce4ad89cac84c5b6286126e3f89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641933"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (biblioteca de R en SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR** es una biblioteca de funciones de ciencia de datos de alto rendimiento de Microsoft. Las funciones admiten la importación de datos, transformación de datos, resúmenes, visualización y análisis.

A diferencia de las funciones de R bases, pueden realizarse operaciones de RevoScaleR en grandes conjuntos de datos en paralelo y en los sistemas de archivos distribuido. Las funciones pueden operar en conjuntos de datos que no caben en memoria mediante la fragmentación y reasigna los resultados cuando se completen las operaciones.

Las funciones de RevoScaleR se denotan con un **rx** o **Rx** prefijo para que sean fáciles de identificar.

RevoScaleR actúa como una plataforma para la ciencia de datos distribuidos. Por ejemplo, puede usar las transformaciones y los contextos de proceso de RevoScaleR con los algoritmos de última generación en [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). También puede usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para ejecutar funciones de base de R en paralelo.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El **RevoScaleR** library se distribuye en varios productos de Microsoft, pero el uso es el mismo si obtener la biblioteca de SQL Server u otro producto. Dado que las funciones son los mismos, [documentación para las funciones de RevoScaleR individuales](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Debe cualquier producto específico comportamientos existen, se anotará discrepancias en la página de Ayuda de la función.

## <a name="versions-and-platforms"></a>Las versiones y plataformas

El **RevoScaleR** biblioteca se basa en R 3.4.3 y disponibles solo al instalar uno de los siguientes productos de Microsoft o descargas:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> Versiones de lanzamiento de producto completo son sólo Windows, a partir de SQL Server 2017. Linux support para **RevoScaleR** es nuevo en [versión preliminar de SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumera las funciones por categoría para darle una idea de cómo se usa cada uno de ellos. También puede usar el [tabla de contenido](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para buscar las funciones en orden alfabético.

## <a name="1-data-source-and-compute"></a>Proceso y el origen de datos 1

**RevoScaleR** incluye funciones para crear orígenes de datos y configuración de la ubicación, o *contexto de proceso*, de donde se realizan los cálculos. Un objeto de origen de datos es un contenedor que especifica una cadena de conexión, junto con el conjunto de datos que quiera, definido como una tabla, una vista o una consulta. No se admiten llamadas a procedimientos almacenados. Las funciones pertinentes para escenarios de SQL Server aparecen en la tabla siguiente.

SQL Server y R usan diferentes tipos de datos en algunos casos. Para obtener una lista de asignaciones entre tipos de datos SQL y R, consulte [tipos de datos de R para SQL](r-libraries-and-data-types.md).

| Función| Descripción|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Crear un objeto de contexto de proceso de SQL Server para enviar los cálculos a una instancia remota. Varios **RevoScaleR** funciones toman el contexto de proceso como un argumento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Obtiene o establece el contexto de cálculo activo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Crear un objeto de datos basado en una consulta de SQL Server o la tabla. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Crear un origen de datos basado en una conexión ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Crear un origen de datos basado en un archivo XDF local. A menudo se usan archivos XDF para descargar datos en memoria en el disco. Un archivo XDF puede ser útil al trabajar con más datos que se pueden transferir desde la base de datos en un lote o más datos que pueden caber en memoria. Por ejemplo, si suele mover grandes cantidades de datos desde una base de datos a una estación de trabajo local, en lugar de consultar la base de datos varias veces para cada operación de R, se puede usar el archivo XDF como una especie de caché para guardar los datos localmente y, a continuación, trabajar con ellos en el área de trabajo de R.|

> [!TIP]
> Si está familiarizado con la idea de los orígenes de datos o contextos de proceso, se recomienda que comience con [informática distribuida](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) en la documentación de Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Siga las instrucciones de DDL

Puede ejecutar instrucciones DDL de R, si tiene los permisos necesarios en la instancia y base de datos. Las siguientes funciones usan llamadas ODBC para ejecutar instrucciones de DDL o recuperar el esquema de base de datos.

| Función| Descripción|
| ------- | ---------- |
| [rxSqlServerTableExists y rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Quitar un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de tabla, o comprobar la existencia de una tabla de base de datos u objeto. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Ejecutar un comando de lenguaje de definición de datos (DDL) que define o usa objetos de base de datos. Esta función no puede devolver datos y sólo se utiliza para recuperar o modificar el esquema de objeto o los metadatos.|

## <a name="2-data-manipulation-etl"></a>Manipulación de datos de 2 (ETL)

Una vez haya creado un objeto de origen de datos, puede utilizar el objeto para cargar datos en él, transformar datos o escribir nuevos datos en el destino especificado. En función del tamaño de los datos en el origen, también puede definir el tamaño del lote como parte del origen de datos y mover los datos en fragmentos.

| Función | Descripción |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Comprobar si un origen de datos está disponible, abra o cierre un origen de datos, leer datos desde un origen, escribir datos en el destino y un origen de datos.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Mover datos desde un origen de datos en almacenamiento de archivos o en una trama de datos.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Transforme los datos mientras se esté moviendo entre orígenes de datos.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>Funciones de gráficos en 3

| Nombre de función | Descripción |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Crea un histograma de datos. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Crea un gráfico de líneas de datos. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcula una curva de Lorenz que se puede trazar. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcula y traza curvas ROC a partir de los datos reales y previstos. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>Estadísticas descriptivas de 4

| Nombre de función | Descripción |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Calcula aproximado cuantiles para archivos xdf y tramas de datos sin ordenar. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Estadísticas de resumen básicas de datos, incluidos cálculos por grupo. Escritura de los cálculos de grupo al archivo xdf no compatible. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Basado en la fórmula de tabulación cruzada de datos. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Alternativo basado en la fórmula de tabulación cruzada diseñado para devolver los resultados del cubo de representación eficaz. Escribir la salida al archivo xdf no compatible. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Resúmenes marginales de valores entre-tabulados. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Convierte los resultados de tabulación cruzada en un objeto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Realiza la prueba de chi cuadrado en el objeto xtabs. Puede usar con conjuntos de datos pequeños y no fragmentar los datos. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Realiza una prueba de exacto de Fisher en objeto xtabs. Puede usar con conjuntos de datos pequeños y no fragmentar los datos. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcula el coeficiente de correlación de Kendall Tau rango mediante el objeto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Aplica una función a combinaciones en pares de filas y columnas de un objeto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcular el riesgo relativo de un objeto xtabs dos por dos. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcula el coeficiente de probabilidades de un objeto xtabs dos por dos. | 

<sup>*</sup> Indica las funciones más populares en esta categoría.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>Funciones de predicción de 5

| Nombre de función | Descripción |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Ajusta un modelo lineal a los datos. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Ajusta un modelo de regresión logística a datos. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Ajusta un modelo lineal generalizado a los datos. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcular la covarianza, correlación o suma de cuadrados o producto vectorial matriz de un conjunto de variables. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Ajusta un árbol de clasificación o regresión a los datos. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Se ajusta a un bosque de decisión de clasificación o regresión a los datos mediante un algoritmo de impulso de gradiente estocástico. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Se ajusta a un bosque de decisión de clasificación o regresión a los datos. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcula predicciones para los modelos ajustados. Salida debe ser un origen de datos XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Realiza la agrupación en clústeres k-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Realiza la clasificación de Naive Bayes. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcular la matriz de covarianza para un conjunto de variables. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcular la correlación de un conjunto de variables. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcular la suma de cuadrados o producto vectorial matriz de un conjunto de variables. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Cálculos de característica (ROC) receptor utilizando los valores reales y previstos de sistema de clasificador binario. | 

<sup>*</sup> Indica las funciones más populares en esta categoría.


## <a name="how-to-work-with-revoscaler"></a>Cómo trabajar con RevoScaleR

Las funciones de **RevoScaleR** son invocables en código R encapsulada en procedimientos almacenados. La mayoría de los desarrolladores crear **RevoScaleR** soluciones localmente, y, a continuación, migrar código de R terminado a los procedimientos almacenados como un ejercicio de implementación.

Cuando se ejecuta localmente, normalmente ejecutar un script de R desde la línea de comandos o desde un entorno de desarrollo de R y especificar un contexto de proceso de SQL Server mediante uno de los **RevoScaleR** funciones. Puede usar el contexto de cálculo remoto para todo el código, o para funciones individuales. Por ejemplo, es posible que desea descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Cuando esté listo para encapsular el script de R dentro de un procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda volver a escribir el código como una sola función que se haya definido claramente las entradas y salidas. 

## <a name="see-also"></a>Vea también

+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Aprenda a usar contextos de cálculo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: Entrenar y uso de modelos](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Muestras de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referencia de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
