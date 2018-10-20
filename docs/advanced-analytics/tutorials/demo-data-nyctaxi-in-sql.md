---
title: Descargue los datos de demostración de taxis de Nueva York y scripts incrustado R y Python (SQL Server Machine Learning) | Microsoft Docs
description: Instrucciones para descargar datos de ejemplo de taxi de Nueva York y crear una base de datos. Datos que se utilizan en los tutoriales de SQL Server que se muestra cómo insertar código de R y Python en SQL Server los procedimientos almacenados y funciones de Transact-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9359bb9a441551d16bc5de3f57f0158e56a98626
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49463060"
---
# <a name="nyc-taxi-demo-data-for-sql-server"></a>Datos de demostración de taxis de Nueva York para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo configurar una base de datos de ejemplo que consta de datos públicos del [ciudad de Nueva York taxis y limusinas Comisión](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml). Estos datos se usan en los tutoriales de varias R y Python para realizar análisis en bases de datos en SQL Server. Los datos de ejemplo están uno por ciento del conjunto de datos público. En el sistema, el archivo de copia de seguridad de base de datos es ligeramente más de 90 MB, proporcionar 1,7 millones de filas en la tabla de datos principal.

Para completar este ejercicio, debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) u otra herramienta que puede restaurar un archivo de copia de seguridad de base de datos y ejecutar consultas de T-SQL.

Tutoriales y guías de inicio rápido con este conjunto de datos incluyen lo siguiente:

+  [Usar un modelo de Python en SQL Server para el entrenamiento y puntuación](train-score-using-python-in-tsql.md)

## <a name="download-demo-database"></a>Descargue la base de datos de demostración

La base de datos de ejemplo es un archivo de copia de seguridad hospedado por Microsoft. Descarga de archivos comienza inmediatamente al hacer clic en el vínculo. 

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
|**NYCTaxi_Sample** | Base de datos |Crea el script create db tb carga data.sql. Crea una base de datos y dos tablas:<br /><br />tabla dbo.nyctaxi_sample: contiene el conjunto de datos NYC Taxi principal. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. El ejemplo de 1% del conjunto de datos NYC Taxi se insertará en esta tabla.<br /><br />tabla dbo.nyc_taxi_models: usa para conservar el modelo de análisis avanzado entrenado.|
|**fnCalculateDistance** |función escalar | Crea el script fnCalculateDistance.sql. Calcula la distancia directa entre las ubicaciones de recogida y destino. Esta función se utiliza en [crear características de datos](sqldev-create-data-features-using-t-sql.md), [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md) y [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |función con valores de tabla | Crea el script fnEngineerFeatures.sql. Crea nuevas características de datos de entrenamiento del modelo. Esta función se utiliza en [crear características de datos](sqldev-create-data-features-using-t-sql.md) y [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**PlotHistogram** |procedimiento almacenado | Crea el script PlotHistogram.sql. Llama a una función de R para trazar el histograma de una variable y, a continuación, devuelve el gráfico como un objeto binario. Este procedimiento almacenado se usa en [explorar y visualizar datos](sqldev-explore-and-visualize-the-data.md).|
|**PlotInOutputFiles** |procedimiento almacenado| Crea el script PlotInOutputFiles.sql. Crea un gráfico mediante una función de R y, a continuación, guarde el resultado como un archivo PDF local. Este procedimiento almacenado se usa en [explorar y visualizar datos](sqldev-explore-and-visualize-the-data.md).|
|**PersistModel** |procedimiento almacenado | Crea el script PersistModel.sql. Toma un modelo que se ha serializado en un tipo de datos varbinary y lo escribe en la tabla especificada. |
|**PredictTip**  |procedimiento almacenado |Crea el script PredictTip.sql. Llama al modelo entrenado para crear predicciones usando el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada. Este procedimiento almacenado se usa en [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**PredictTipSingleMode**  |procedimiento almacenado| Crea el script PredictTipSingleMode.sql. Llama al modelo entrenado para crear predicciones usando el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación. Este procedimiento almacenado se usa en [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**TrainTipPredictionModel**  |procedimiento almacenado|Crea el script TrainTipPredictionModel.sql. Entrena un modelo de regresión logística mediante una llamada a un paquete de R. El modelo predice el valor de la columna tipped y se entrena usando un 70 % de los datos seleccionados aleatoriamente. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models. Este procedimiento almacenado se usa en [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md).|

## <a name="query-data-for-verification"></a>Consultar los datos para la comprobación

Como paso de validación, ejecute una consulta para confirmar que se han cargado los datos.

1. En el Explorador de objetos, en las bases de datos, haga clic en el **NYCTaxi_Sample** , inicie una nueva consulta y base de datos.

2. Ejecute algunas consultas sencillas:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
La base de datos contiene 1,7 millones de filas.

## <a name="next-steps"></a>Pasos siguientes

Datos de ejemplo de taxis de Nueva York ahora están disponibles para el aprendizaje práctico.

+ [Obtenga información sobre los análisis en bases de datos con R en SQL Server](sqldev-in-database-r-for-sql-developers.md)