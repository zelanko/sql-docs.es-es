---
title: Paquete RevoScaleR de R
description: RevoScaleR es un paquete de R de Microsoft que admite computación distribuida, contextos de cálculo remoto y algoritmos de ciencia de datos de alto rendimiento. También admite la importación de datos, la transformación de datos, el resumen, la visualización y el análisis. El paquete se incluye en SQL Server Machine Learning Services y en SQL Server 2016 R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 87d4fbcfa114b9f80f19495b3d3728c2dd7678ac
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470836"
---
# <a name="revoscaler-r-package-in-sql-server-machine-learning-services"></a>RevoScaleR (paquete de R en SQL Server Machine Learning Services)

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**RevoScaleR** es un paquete de R de Microsoft que admite computación distribuida, contextos de cálculo remoto y algoritmos de ciencia de datos de alto rendimiento. También admite la importación de datos, la transformación de datos, el resumen, la visualización y el análisis. El paquete se incluye en [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) y en [SQL Server 2016 R Services](sql-server-r-services.md).

A diferencia de las funciones base de R, las operaciones de RevoScaleR se pueden realizar en conjuntos de datos grandes, en paralelo y en sistemas de archivos distribuidos. Las funciones pueden operar en conjuntos de valores que no caben en la memoria mediante fragmentación y reensamblado de los resultados cuando se completan las operaciones.

Las funciones de RevoScaleR se indican con un prefijo rx** o **RX** para que sean fáciles de identificar.

RevoScaleR sirve como plataforma para la ciencia de datos distribuidos. Por ejemplo, puede usar las transformaciones y contextos de cálculo de RevoScaleR con los algoritmos de última generación de [MicrosoftML](/machine-learning-server/r/concept-what-is-the-microsoftml-package). También puede usar [rxExec](/machine-learning-server/r-reference/revoscaler/rxexec) para ejecutar funciones base de R en paralelo.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El paquete de **RevoScaleR** se distribuye en varios productos de Microsoft, pero el uso es el mismo, se obtenga el paquete en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia de R](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

El paquete de **RevoScaleR** se basa en R 3.4.3 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](/machine-learning-server/)
+ [Cliente de Microsoft R](set-up-a-data-science-client.md)

> [!NOTE]
> En SQL Server 2017, las versiones completas del producto son solo para Windows. Para **RevoScaleR** en [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md), se admiten tanto Windows como Linux.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría, para darle una idea del uso de cada una de ellas. También puede usar la [tabla de contenido](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para ver las funciones en orden alfabético.

## <a name="1-data-source-and-compute"></a>1- Origen de datos y cálculo

**RevoScaleR** incluye funciones para crear orígenes de datos y establecer la ubicación, o el *contexto de proceso*, de dónde se realizan los cálculos. Un objeto de origen de datos es un contenedor que especifica una cadena de conexión, junto con el conjunto de datos que quiera, definido como una tabla, una vista o una consulta. No se admiten llamadas a procedimientos almacenados. En la tabla siguiente se enumeran las funciones relevantes para los escenarios de SQL Server.

En algunos casos, SQL Server y R usan tipos de datos diferentes. Para obtener una lista de las asignaciones entre los tipos de datos de SQL y R, vea [tipos de datos entre R y SQL](r-libraries-and-data-types.md).

| Función| Descripción|
| ------- | ---------- |
| [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Cree un objeto de contexto de proceso de SQL Server para enviar los cálculos a una instancia remota. Varias funciones de **RevoScaleR** toman el contexto de proceso como argumento. |
|[rxGetComputeContext / rxSetComputeContext](/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Obtenga o establezca el contexto de proceso activo. |
| [RxSqlServerData](/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Cree un objeto de datos basado en una consulta o una tabla de SQL Server. |
| [RxOdbcData](/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Cree un origen de datos basado en una conexión ODBC. |
| [RxXdfData](/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Cree un origen de datos basado en un archivo XDF local. Los archivos XDF a menudo se usan para descargar en el disco los datos en memoria. Un archivo XDF puede ser útil al trabajar con más datos de los que se pueden transferir desde la base de datos en un lote o con más datos de los que caben en la memoria. Por ejemplo, si suele mover grandes cantidades de datos de una base de datos a una estación de trabajo local, en lugar de consultar la base de datos varias veces para cada operación de R, puede usar el archivo XDF a modo de memoria caché para guardar los datos localmente y, después, trabajar con ellos en el área de trabajo de R.|

> [!TIP]
> Si no está familiarizado con la idea de los orígenes de datos o los contextos de cálculo, le recomendamos que comience con la [computación distribuida](/machine-learning-server/r/how-to-revoscaler-distributed-computing) en la documentación de Microsoft Machine Learning Server.

### <a name="perform-ddl-statements"></a>Ejecutar instrucciones DDL

Puede ejecutar instrucciones de DDL de R si tiene los permisos necesarios en la instancia y la base de datos. Las siguientes funciones usan las llamadas ODBC para ejecutar instrucciones DDL o recuperar el esquema de la base de datos.

| Función| Descripción|
| ------- | ---------- |
| [rxSqlServerTableExists y rxSqlServerDropTable](/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Elimine una tabla [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o compruebe la existencia de un objeto o una tabla de base de datos. |
| [rxExecuteSQLDDL](/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Ejecute un comando de lenguaje de definición de datos (DDL) que defina o manipule objetos de base de datos. Esta función no puede devolver datos y solo se usa para recuperar o modificar el esquema de objetos o los metadatos.|

## <a name="2-data-manipulation-etl"></a>2- Manipulación de datos (ETL)

Después de crear un objeto de origen de datos, puede usar el objeto para cargar datos en él, transformar los datos o escribir otros nuevos en el destino especificado. En función del tamaño de los datos en el origen, también puede definir el tamaño del lote como parte del origen de datos y mover los datos en fragmentos.

| Función | Descripción |
|----------|-------------|
| [rxOpen-methods](/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Compruebe si un origen de datos está disponible, abre o cierra un origen de datos, lee los datos de un origen, escribe datos en el destino y cierra un origen de datos.|
| [rxImport](/machine-learning-server/r-reference/revoscaler/rximport) | Mueva los datos desde un origen de datos al almacenamiento de archivos o a una trama de datos.|
| [rxDataStep](/machine-learning-server/r-reference/revoscaler/rxdatastep) | Transforme los datos mientras los mueve entre orígenes de datos.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3- Funciones de creación de gráficos

| Nombre de función | Descripción |
|---------------|-------------|
|[rxHistogram](/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Crea un histograma a partir de los datos. | 
|[rxLinePlot](/machine-learning-server/r-reference/revoscaler/rxlineplot) |Crea un gráfico de líneas a partir de los datos. | 
|[rxLorenz](/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcula una curva de Lorenz que se puede mostrar como un trazado. | 
|[rxRocCurve](/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcula y traza curvas ROC a partir de los datos reales y previstos. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4- Estadísticas descriptivas

| Nombre de función | Descripción |
|---------------|-------------|
|[rxQuantile](/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |Calcula los cuantiles aproximados para archivos .xdf y tramas de datos sin ordenar. | 
|[rxSummary](/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |Estadísticas de resumen básico de datos, incluidos los cálculos por grupo. No se admite la escritura de cálculos de grupo en el archivo .xdf. | 
|[rxCrossTabs](/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Tabulación cruzada basada en fórmulas de los datos. | 
|[rxCube](/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |Tabulación cruzada basada en fórmulas alternativa diseñada para la representación eficaz que devuelve resultados del cubo. No se admite la escritura de resultados en el archivo .xdf. | 
|[rxMarginals](/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Resúmenes marginales de las tabulaciones cruzadas. | 
|[as.xtabs](/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Convierte los resultados de tabulación cruzada en un objeto xtabs. | 
|[rxChiSquaredTest](/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Realiza una prueba χ2 en un objeto xtabs. Se usa con conjuntos de datos pequeños y no fragmenta los datos. | 
|[rxFisherTest](/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Realiza una prueba de exacto de Fisher en un objeto xtabs. Se usa con conjuntos de datos pequeños y no fragmenta los datos. | 
|[rxKendallCor](/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcula el coeficiente de correlación por rangos tau de Kendall mediante un objeto xtabs. | 
|[rxPairwiseCrossTab](/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Aplica una función a combinaciones por pares de filas y columnas de un objeto xtabs. | 
|[rxRiskRatio](/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcula el riesgo relativo de un objeto xtabs de dos por dos. | 
|[rxOddsRatio](/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcula el coeficiente de probabilidades de un objeto xtabs de dos por dos. | 

<sup>*</sup> Indica las funciones más populares de esta categoría.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5- Funciones de predicción

| Nombre de función | Descripción |
|---------------|-------------|
|[rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Ajusta un modelo lineal a los datos. | 
|[rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Ajusta un modelo de regresión logística a los datos. | 
|[rxGlm](/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Ajusta un modelo lineal generalizado a los datos. | 
|[rxCovCor](/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcula la covarianza, correlación o la matriz de suma de cuadrados o producto vectorial de un conjunto de variables. | 
|[rxDTree](/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Ajusta un árbol de clasificación o regresión a los datos. | 
|[rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Ajusta un bosque de decisión de clasificación o regresión a los datos mediante un algoritmo de potenciación del gradiente estocástico. | 
|[rxDForest](/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |Ajusta un bosque de decisión de clasificación o regresión a los datos. | 
|[rxPredict](/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |Calcula predicciones para los modelos ajustados. La salida debe ser un origen de datos XDF. | 
|[rxKmeans](/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |Lleva a cabo la agrupación en clústeres k-means. | 
|[rxNaiveBayes](/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Realiza una clasificación de Naive Bayes. | 
|[rxCov](/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcula la matriz de covarianza de un conjunto de variables. | 
|[rxCor](/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcula la matriz de correlación de un conjunto de variables. | 
|[rxSSCP](/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcula la matriz de suma de cuadrados o producto vectorial de un conjunto de variables. | 
|[rxRoc](/machine-learning-server/r-reference/revoscaler/rxroc)  |Cálculos de una característica operativa del receptor (ROC) con los valores reales y previstos de un sistema clasificador binario. | 

<sup>*</sup> Indica las funciones más populares de esta categoría.


## <a name="how-to-work-with-revoscaler"></a>Cómo trabajar con RevoScaleR

Las funciones de **RevoScaleR** se pueden llamar en código R encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones de **RevoScaleR** localmente y, después, migran el código R final a los procedimientos almacenados como un ejercicio de implementación.

Cuando se ejecuta localmente, normalmente se ejecuta un script de R desde la línea de comandos o desde un entorno de desarrollo de R, y se especifica un contexto de proceso de SQL Server mediante una de las funciones de **RevoScaleR**. Puede usar el contexto de proceso remoto para todo el código o para funciones individuales. Por ejemplo, puede que quiera descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Cuando esté preparado para encapsular el script de R dentro de un procedimiento almacenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), se recomienda que vuelva a escribir el código como una sola función que tenga las entradas y salidas definidas con claridad. 

## <a name="see-also"></a>Consulte también

+ [Tutoriales de R](../tutorials/r-tutorials.md)
+ [Información sobre cómo usar contextos de cálculo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: Entrenar y hacer operativo un modelo](../tutorials/r-taxi-classification-introduction.md)
+ [Ejemplos de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referencia de R (Microsoft Machine Learning Server)](/machine-learning-server/r-reference/introducing-r-server-r-package-reference)