---
title: Uso de PowerShell (aprendizaje automático de SQL Server) el entorno de la lección 2 preparar R tutorial | Documentos de Microsoft
description: Tutorial que muestra cómo incrustar R en SQL Server los procedimientos almacenados y funciones de T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1280d7c82d48c8ed596271cd7a73fa13ec1664c7
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249748"
---
# <a name="lesson-2-set-up-the-tutorial-environment-using-powershell"></a>Lección 2: Configurar el entorno de tutorial con PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, va a ejecutar un script de PowerShell para crear los objetos de base de datos necesarios para el tutorial. El script se crea y carga una base de datos con datos de ejemplo obtenidos en el paso anterior. También crea funciones y procedimientos almacenados que se utilizan a lo largo del tutorial.

## <a name="create-and-load-database-objects"></a>Crear y cargar los objetos de base de datos

Entre los archivos descargados, debería ver un script de PowerShell (`RunSQL_SQL_Walkthrough.ps1`) que prepara el entorno para el tutorial. Las acciones realizadas por el script son las siguientes:

- Instale el cliente nativo de SQL y utilidades de línea de comandos de SQL, si aún no está instalado. Estas utilidades son necesarias para la carga masiva de los datos en la mediante **bcp**.

- Crear una base de datos y tablas en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instancia y los datos obtenidos de un archivo .csv de inserción masiva.

- Crear varios procedimientos almacenados y funciones SQL.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>Modifique el script para usar una identidad de Windows de confianza

De forma predeterminada, el script asume que un inicio de sesión de usuario de base de datos de SQL Server y una contraseña. Si estás db_owner en su cuenta de usuario de Windows, puede usar la identidad de Windows para crear los objetos. Para ello, abra `RunSQL_SQL_Walkthrough.ps1` en un editor de código y anexar **`-T`** a bcp bulk insert, comando (línea 238):

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>Ejecute el script para crear objetos

Abra un símbolo del sistema de PowerShell como administrador y ejecute el siguiente comando.
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
Deberá introducir la información siguiente:

- Instancia de servidor donde [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se ha instalado. En una instancia predeterminada, esto puede ser tan simple como el nombre del equipo.

- Nombre de base de datos. Para este tutorial, secuencias de comandos asumen `TaxiNYC_Sample`.

- Nombre de usuario y la contraseña de usuario. Escriba un inicio de sesión de base de datos de SQL Server para estos valores. O bien, si ha modificado la secuencia de comandos para que acepte una identidad de Windows de confianza, presione ENTRAR para dejar estos valores en blanco. La identidad de Windows se utiliza en la conexión.

- Nombre de archivo completo para los datos de ejemplo que descargó en la lección anterior. Por ejemplo, `C:\tempRSQL\nyctaxi1pct.csv`

Después de proporcionar estos valores, el script se ejecuta inmediatamente. Durante la ejecución de secuencias de comandos, todos los nombres de marcador de posición en el [!INCLUDE[tsql](../../includes/tsql-md.md)] se actualizan las secuencias de comandos para usar las entradas que proporcione.

## <a name="review-database-objects"></a>Revise los objetos de base de datos
   
Cuando haya finalizado la ejecución del script, asegúrese de que los objetos de base de datos se encuentran en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Debería ver la base de datos, tablas, funciones y procedimientos almacenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> Si los objetos de base de datos ya existen, no se pueden crear de nuevo.
>   
> Si la tabla ya existe, los datos se anexarán, no se sobrescriben. Por tanto, asegúrese de quitar todos los objetos existentes antes de ejecutar el script.

## <a name="objects-used-in-this-tutorial"></a>Objetos que se utilizan en este tutorial

En la tabla siguiente se resume los objetos creados en esta lección. Aunque solo es posible ejecutar un script de PowerShell (`RunSQL_SQL_Walkthrough.ps1`), ese script llama a otras secuencias de comandos SQL a su vez para crear los objetos en la base de datos. Las secuencias de comandos que se utiliza para crear cada objeto se mencionan en la descripción.

|**Nombre de objeto**|**Tipo de objeto**|**Descripción**|
|----------|------------------------|---------------|
|**TaxiNYC_Sample** | Base de datos |Creado por el script de creación db tb carga data.sql. Crea una base de datos y dos tablas:<br /><br />tabla dbo.nyctaxi_sample: contiene el conjunto de datos principal de Nueva York Taxi. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. En esta tabla se inserta en el ejemplo de 1% del conjunto de datos de Nueva York Taxi.<br /><br />tabla dbo.nyc_taxi_models: utiliza para conservar el modelo entrenado análisis avanzados.|
|**fnCalculateDistance** |función escalar | Crea el script fnCalculateDistance.sql. Calcula la distancia entre las ubicaciones de recogida y caída directa. Esta función se utiliza en [crear características de datos](../tutorials/sqldev-create-data-features-using-t-sql.md), [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md) y [poner el modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |función con valores de tabla | Crea el script fnEngineerFeatures.sql. Crea nuevas características de datos de entrenamiento del modelo. Esta función se utiliza en [crear características de datos](../tutorials/sqldev-create-data-features-using-t-sql.md) y [poner el modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**PlotHistogram** |procedimiento almacenado | Crea el script PlotHistogram.sql. Llama a una función de R para trazar el histograma de una variable y, a continuación, devuelve el gráfico como un objeto binario. Este procedimiento almacenado se utiliza en [explorar y visualizar datos](../tutorials/sqldev-explore-and-visualize-the-data.md).|
|**PlotInOutputFiles** |procedimiento almacenado| Crea el script PlotInOutputFiles.sql. Crea un gráfico utilizando una función de R y, a continuación, guarde el resultado como un archivo PDF local. Este procedimiento almacenado se utiliza en [explorar y visualizar datos](../tutorials/sqldev-explore-and-visualize-the-data.md).|
|**PersistModel** |procedimiento almacenado | Crea el script PersistModel.sql. Toma un modelo que se ha serializado en un tipo de datos varbinary y lo escribe en la tabla especificada. |
|**PredictTip**  |procedimiento almacenado |Crea el script PredictTip.sql. Llama al modelo entrenado para crear predicciones utilizando el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada. Este procedimiento almacenado se utiliza en [poner el modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**PredictTipSingleMode**  |procedimiento almacenado| Crea el script PredictTipSingleMode.sql. Llama al modelo entrenado para crear predicciones utilizando el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación. Este procedimiento almacenado se utiliza en [poner el modelo R](../tutorials/sqldev-operationalize-the-model.md).|
|**TrainTipPredictionModel**  |procedimiento almacenado|Crea el script TrainTipPredictionModel.sql. Entrena un modelo de regresión logística mediante una llamada a un paquete de R. El modelo predice el valor de la columna tipped y se entrena usando un 70 % de los datos seleccionados aleatoriamente. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models. Este procedimiento almacenado se utiliza en [entrenar y guardar un modelo](sqldev-train-and-save-a-model-using-t-sql.md).|

## <a name="next-lesson"></a>Lección siguiente

[Lección 3: Explorar y visualizar los datos](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 1: Descargar los datos de ejemplo](../tutorials/sqldev-download-the-sample-data.md)
