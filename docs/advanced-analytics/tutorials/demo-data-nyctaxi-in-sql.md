---
title: Descargue los scripts y los datos de demostración de taxis de Nueva York para R y Python incrustados
description: Instrucciones para descargar datos de ejemplo de taxis de Nueva York y crear una base de datos. Los datos se usan en los tutoriales del lenguaje SQL Server Python y R que muestran cómo insertar un script en SQL Server procedimientos almacenados y funciones de T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5b60397bb3581ba2d210a6b4469184306145c8a
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714865"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>Datos de demostración de taxis de Nueva York para tutoriales de SQL Server Python y R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se explica cómo configurar una base de datos de ejemplo que consta de datos públicos de la [Comisión de taxi y limusinas de Nueva York](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Estos datos se usan en varios tutoriales de R y Python para análisis de bases de datos en SQL Server. Para que el código de ejemplo se ejecute más rápido, creamos una muestra representativa del 1% de los datos. En el sistema, el archivo de copia de seguridad de base de datos es ligeramente superior a 90 MB, lo que proporciona 1,7 millones filas en la tabla de datos principal.

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que pueda restaurar un archivo de copia de seguridad de base de datos y ejecutar consultas de T-SQL.

Entre los tutoriales y las guías de inicio rápido que usan este conjunto de datos se incluyen los siguientes:

+ [Obtenga información sobre el análisis de bases de datos con R en SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Obtenga información sobre el análisis de bases de datos con Python en SQL Server](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>Descargar archivos

La base de datos de ejemplo es un archivo SQL Server 2016 BAK hospedado por Microsoft. Puede restaurarlo en SQL Server 2016 y versiones posteriores. La descarga de archivos comienza inmediatamente al hacer clic en el vínculo. 

El tamaño del archivo es de aproximadamente 90 MB.

1. Haga clic en [NYCTaxi_Sample. bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) para descargar el archivo de copia de seguridad de base de datos.

2. Copie el archivo en la carpeta C:\Archivos de Programa\microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup

3. En Management Studio, haga clic con el botón derecho en **bases de datos** y seleccione **restaurar archivos y grupos de archivos**.

4. Escriba *NYCTaxi_Sample* como nombre de la base de datos.

5. Haga clic en **desde dispositivo** y, a continuación, abra la página selección de archivos para seleccionar el archivo de copia de seguridad. Haga clic en **Agregar** para seleccionar NYCTaxi_Sample. bak.

6. Active la casilla **restaurar** y haga clic en **Aceptar** para restaurar la base de datos.

## <a name="review-database-objects"></a>Revisar objetos de base de datos
   
Confirme que los objetos de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos existen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]en la instancia de mediante. Debería ver la base de datos, las tablas, las funciones y los procedimientos almacenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>Objetos de la base de datos NYCTaxi_Sample

En la tabla siguiente se resumen los objetos creados en la base de datos de demostración de taxi de Nueva York.

|**Nombre de objeto**|**Tipo de objeto**|**Descripción**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | Crea una base de datos y dos tablas:<br /><br />tabla DBO. nyctaxi_sample: Contiene el conjunto de Nueva York de taxi principal. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. En esta tabla se inserta el ejemplo 1% del conjunto de Nueva York taxi.<br /><br />tabla DBO. Nueva York _taxi_models: Se usa para conservar el modelo de análisis avanzado entrenado.|
|**fnCalculateDistance** |función escalar | Calcula la distancia directa entre las ubicaciones de recogida y recogida. Esta función se utiliza en [las características de creación de datos](sqldev-create-data-features-using-t-sql.md), [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md) y poner en [funcionamiento el modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |función con valores de tabla | Crea nuevas características de datos para el entrenamiento del modelo. Esta función se usa en [las características de creación de datos](sqldev-create-data-features-using-t-sql.md) y en [el modelo de R](sqldev-operationalize-the-model.md).|


Los procedimientos almacenados se crean mediante el script de R y Python que se encuentra en varios tutoriales. En la tabla siguiente se resumen los procedimientos almacenados que se pueden agregar opcionalmente a la base de datos de demostración de taxis de Nueva York cuando se ejecuta un script desde diversas lecciones.

|**Procedimiento almacenado**|**Lenguaje**|**Descripción**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | Llama a la función rxHistogram de RevoScaleR para trazar el histograma de una variable y, a continuación, devuelve el trazado como un objeto binario. Este procedimiento almacenado se usa en [explorar y visualizar los datos](sqldev-explore-and-visualize-the-data.md).|
|**RPlotRHist** |R| Crea un gráfico con la función de hist y guarda el resultado como un archivo PDF local. Este procedimiento almacenado se usa en [explorar y visualizar los datos](sqldev-explore-and-visualize-the-data.md).|
|**RxTrainLogitModel**  |R| Entrena un modelo de regresión logística llamando a un paquete de R. El modelo predice el valor de la columna tipped y se entrena usando un 70 % de los datos seleccionados aleatoriamente. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models. Este procedimiento almacenado se utiliza para [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md).|
|**RxPredictBatchOutput**  |R | Llama al modelo entrenado para crear predicciones mediante el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada. Este procedimiento almacenado se usa en los [resultados de predicción potenciales](sqldev-operationalize-the-model.md).|
|**RxPredictSingleRow**  |R| Llama al modelo entrenado para crear predicciones mediante el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación. Este procedimiento almacenado se usa en los [resultados de predicción potenciales](sqldev-operationalize-the-model.md).|

## <a name="query-the-data"></a>Consultar los datos

Como paso de validación, ejecute una consulta para confirmar que se cargaron los datos.

1. En Explorador de objetos, en bases de datos, haga clic con el botón secundario en la base de datos **NYCTaxi_Sample** e inicie una nueva consulta.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
La base de datos contiene 1,7 millones filas.

3. Dentro de la base de datos hay una tabla **nyctaxi_sample** que contiene el conjunto de datos. La tabla se ha optimizado para cálculos basados en conjuntos con la adición de un [Índice de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md). Ejecute esta instrucción para generar un resumen rápido de la tabla.

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
Los resultados deberían ser similares a los que se muestran en la captura de pantalla siguiente.

  ![Información de Resumen de tabla](media/nyctaxidatatablesummary.png "Resultados") de la consulta

## <a name="next-steps"></a>Pasos siguientes

Los datos de ejemplo de taxis de Nueva York ahora están disponibles para el aprendizaje práctico.

+ [Obtenga información sobre el análisis de bases de datos con R en SQL Server](sqldev-in-database-r-for-sql-developers.md)
+ [Obtenga información sobre el análisis de bases de datos con Python en SQL Server](sqldev-in-database-python-for-sql-developers.md)