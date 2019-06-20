---
title: Descargue datos de demostración de taxis de Nueva York y scripts incrustado R y Python - SQL Server Machine Learning
description: Instrucciones para descargar datos de ejemplo de taxi de Nueva York y crear una base de datos. Datos se utilizan en los tutoriales de lenguaje Python de SQL Server y R que se muestra cómo incrustar secuencias de comandos en las funciones de Transact-SQL y procedimientos almacenados de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 502f46b67dbf282a7b3daeac76882915a7c3ac84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "64505445"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Datos de taxis de Nueva York demostración para ver tutoriales de Python de SQL Server y R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo configurar una base de datos de ejemplo que consta de datos públicos del [ciudad de Nueva York taxis y limusinas Comisión](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Estos datos se usan en los tutoriales de varias R y Python para realizar análisis en bases de datos en SQL Server. Para que el código de ejemplo se ejecute con mayor rapidez, hemos creado una muestra representativa del 1% de los datos. En el sistema, el archivo de copia de seguridad de base de datos es ligeramente más de 90 MB, proporcionar 1,7 millones de filas en la tabla de datos principal.

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que puede restaurar un archivo de copia de seguridad de base de datos y ejecutar consultas de T-SQL.

Tutoriales y guías de inicio rápido con este conjunto de datos incluyen lo siguiente:

+ [Obtenga información sobre los análisis en bases de datos con R en SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Obtenga información sobre los análisis en bases de datos con Python en SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Descargar archivos

La base de datos de ejemplo es un archivo de SQL Server 2016 BAK hospedado por Microsoft. Se puede restaurar en SQL Server 2016 y versiones posteriores. Descarga de archivos comienza inmediatamente al hacer clic en el vínculo. 

Tamaño del archivo es de aproximadamente 90 MB.

1. Haga clic en [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) para descargar el archivo de copia de seguridad de base de datos.

2. Copie el archivo en C:\Program files\Microsoft SQL Server\MSSQL-instancia-name\MSSQL\Backup carpeta.

3. En Management Studio, haga clic en **bases de datos** y seleccione **restaurar archivos y grupos de archivos**.

4. Escriba *NYCTaxi_Sample* como el nombre de la base de datos.

5. Haga clic en **desde dispositivo** y, a continuación, abra la página de selección para seleccionar el archivo de copia de seguridad. Haga clic en **agregar** seleccionar NYCTaxi_Sample.bak.

6. Seleccione el **restaurar** casilla y haga clic en **Aceptar** para restaurar la base de datos.

## <a name="review-database-objects"></a>Revise los objetos de base de datos
   
Asegúrese de los objetos de base de datos se encuentran en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Debería ver la base de datos, tablas, funciones y procedimientos almacenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Objetos de base de datos NYCTaxi_Sample

En la tabla siguiente se resume los objetos creados en la base de datos de demostración de taxis de Nueva York.

|**Nombre de objeto**|**Tipo de objeto**|**Descripción**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | Crea una base de datos y dos tablas:<br /><br />tabla dbo.nyctaxi_sample: Contiene el conjunto de datos NYC Taxi principal. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. El ejemplo de 1% del conjunto de datos NYC Taxi se insertará en esta tabla.<br /><br />tabla dbo.nyc_taxi_models: Se usa para conservar el modelo de análisis avanzado entrenado.|
|**fnCalculateDistance** |función escalar | Calcula la distancia directa entre las ubicaciones de recogida y destino. Esta función se utiliza en [crear características de datos](sqldev-create-data-features-using-t-sql.md), [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md) y [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |función con valores de tabla | Crea nuevas características de datos de entrenamiento del modelo. Esta función se utiliza en [crear características de datos](sqldev-create-data-features-using-t-sql.md) y [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|


Los procedimientos almacenados se crean mediante comandos de R y Python que se encuentra en diversos tutoriales. En la tabla siguiente se resume los procedimientos almacenados que se pueden agregar a la base de datos de demostración de taxis de Nueva York, opcionalmente, cuando se ejecuta el script desde varias lecciones.

|**procedimiento almacenado**|**Lenguaje**|**Descripción**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Llama a la función de RevoScaleR rxHistogram para trazar el histograma de una variable y, a continuación, devuelve el gráfico como un objeto binario. Este procedimiento almacenado se usa en [explorar y visualizar datos](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Crea un gráfico mediante la función Hist y guarda el resultado como un archivo PDF local. Este procedimiento almacenado se usa en [explorar y visualizar datos](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Entrena un modelo de regresión logística mediante una llamada a un paquete de R. El modelo predice el valor de la columna tipped y se entrena usando un 70 % de los datos seleccionados aleatoriamente. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models. Este procedimiento almacenado se usa en [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Llama al modelo entrenado para crear predicciones usando el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada. Este procedimiento almacenado se usa en [predecir los resultados posibles](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Llama al modelo entrenado para crear predicciones usando el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación. Este procedimiento almacenado se usa en [predecir los resultados posibles](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se han cargado los datos.

1. En el Explorador de objetos, en las bases de datos, haga clic en el **NYCTaxi_Sample** , inicie una nueva consulta y base de datos.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
La base de datos contiene 1,7 millones de filas.

3. Dentro de la base de datos es un **nyctaxi_sample** tabla que contiene el conjunto de datos. La tabla se ha optimizado para cálculos basados en conjunto con la adición de un [índice de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md). Ejecute esta instrucción para generar un resumen rápido en la tabla.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
Resultados deben ser similares a los que se muestra en la captura de pantalla siguiente.

  ![Información de resumen de la tabla](media/nyctaxidatatablesummary.png "resultados de la consulta")

## <a name="next-steps"></a>Pasos siguientes

Datos de ejemplo de taxis de Nueva York ahora están disponibles para el aprendizaje práctico.

+ [Obtenga información sobre los análisis en bases de datos con R en SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Obtenga información sobre los análisis en bases de datos con Python en SQL Server](sqldev-in-database-python-for-sql-developers.md)