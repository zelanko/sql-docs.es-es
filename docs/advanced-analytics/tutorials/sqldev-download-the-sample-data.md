---
title: Descargue los datos de demostración de taxis de Nueva York y scripts incrustado R y Python (SQL Server Machine Learning) | Microsoft Docs
description: Instrucciones para descargar datos de ejemplo de taxi de Nueva York y crear una base de datos. Datos que se utilizan en los tutoriales de SQL Server que se muestra cómo insertar código de R y Python en SQL Server los procedimientos almacenados y funciones de Transact-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 58a996ae500a27a6878b30fc072bf09a75d4ba43
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712758"
---
# <a name="nyc-taxi-demo-data-for-sql-server"></a>Datos de demostración de taxis de Nueva York para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se prepara el sistema para ver tutoriales sobre cómo usar R y Python para realizar análisis en bases de datos en SQL Server.

En este ejercicio, se descargará los datos de ejemplo, un script de PowerShell para preparar el entorno, y [!INCLUDE[tsql](../../includes/tsql-md.md)] usados en varios tutoriales de archivos de script. Cuando haya terminado, un **NYCTaxi_Sample** base de datos está disponible en la instancia local, y proporciona datos de demostración para obtener conocimientos prácticos. 

## <a name="prerequisites"></a>Requisitos previos

Necesitará una conexión a internet, PowerShell y los derechos administrativos locales en el equipo. Debe tener [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) u otra herramienta para comprobar la creación de objetos.

## <a name="download-nyc-taxi-demo-data-and-scripts-from-github"></a>Descargue los datos de demostración de taxis de Nueva York y scripts desde Github

1.  Abra una consola de comandos de Windows PowerShell.
  
    Use la **ejecutar como administrador** opción para crear el directorio de destino o para escribir archivos en el destino especificado.
  
2.  Ejecute los siguientes comandos de PowerShell, y cambie el valor del parámetro *DestDir* por cualquier directorio local. El valor predeterminado que hemos usado aquí es **TempRSQL**.
  
    ```ps
    $source = ‘https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_SQL_Walkthrough.ps1’  
    $ps1_dest = “$pwd\Download_Scripts_SQL_Walkthrough.ps1”
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQL_Walkthrough.ps1 –DestDir ‘C:\tempRSQL’
    ```
  
    Si la carpeta que especifique en *DestDir* no existe, el script de PowerShell la creará.
  
    > [!TIP]
    > Si se produce un error, puede establecer temporalmente la directiva para la ejecución de scripts de PowerShell para **sin restricciones** solo para este tutorial utilizando el argumento de omisión y definir el ámbito de los cambios en la sesión actual.
    >   
    >````
    > Set\-ExecutionPolicy Bypass \-Scope Process
    >````
    > Ejecutar este comando no produce un cambio de configuración.
  
    Dependiendo de la conexión a Internet, es posible que la descarga tarde un rato.
  
3.  Cuando se han descargado todos los archivos, el script de PowerShell se abre en el *DestDir* carpeta. En el símbolo del sistema de PowerShell, ejecute el siguiente comando y revise los archivos que se han descargado.
  
    ```
    ls
    ```
  
    **Resultados:**
  
    ![lista de los archivos descargados por el script de PowerShell](media/rsql-devtut-filelist.png "lista de los archivos descargados por el script de PowerShell")

## <a name="create-nyctaxisample-database"></a>Crear base de datos NYCTaxi_Sample

Entre los archivos descargados, debería ver un script de PowerShell (**RunSQL_SQL_Walkthrough.ps1**) que crea una base de datos y carga de forma masiva de datos. Las acciones realizadas por el script son las siguientes:

+ Instala el SQL Native Client y utilidades de línea de comandos de SQL, si aún no está instalado. Estas utilidades son necesarias para la carga masiva de los datos en la mediante **bcp**.

+ Crear una base de datos y tablas en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instancia y un archivo .csv como originadas de datos de inserción masiva.

+ Crear varias funciones de SQL y procedimientos almacenados utilizados en varios tutoriales.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>Modifique el script para usar una identidad de Windows de confianza

De forma predeterminada, el script supone un inicio de sesión de usuario de base de datos de SQL Server y una contraseña. Si estás db_owner en la cuenta de usuario de Windows, puede usar la identidad de Windows para crear los objetos. Para ello, abra `RunSQL_SQL_Walkthrough.ps1` en un editor de código y anexe **`-T`** a bcp bulk insert (línea 238) del comando:

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script-to-create-objects"></a>Ejecute el script para crear objetos

Con un símbolo del sistema de PowerShell de administrador en C:\tempRSQL, ejecute el siguiente comando.
  
```ps
.\RunSQL_SQL_Walkthrough.ps1
```
Se le pedirá que escriba la siguiente información:

- Instancia de servidor donde [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se ha instalado. En una instancia predeterminada, esto puede ser tan simple como el nombre del equipo.

- Nombre de base de datos. Para este tutorial, secuencias de comandos asumen `NYCTaxi_Sample`.

- Nombre de usuario y contraseña de usuario. Escriba un inicio de sesión de base de datos de SQL Server para estos valores. Como alternativa, si modifica la secuencia de comandos para que acepte una identidad de Windows de confianza, presione ENTRAR para dejar estos valores en blanco. La identidad de Windows se usa en la conexión.

- Nombre de archivo completo de los datos de ejemplo descargados en la lección anterior. Por ejemplo, `C:\tempRSQL\nyctaxi1pct.csv`

Después de proporcionar estos valores, el script se ejecuta inmediatamente. Durante la ejecución de secuencia de comandos, todos los nombres de marcador de posición en el [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos se actualizan para usar las entradas que proporcione.

## <a name="review-database-objects"></a>Revise los objetos de base de datos
   
Cuando haya finalizado la ejecución del script, confirme que los objetos de base de datos existen en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Debería ver la base de datos, tablas, funciones y procedimientos almacenados.
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

> [!NOTE]
> Si los objetos de base de datos ya existen, no se pueden crear de nuevo.
>   
> Si la tabla ya existe, los datos se anexarán, no se sobrescriben. Por tanto, asegúrese de quitar todos los objetos existentes antes de ejecutar el script.

### <a name="objects-in-nyctaxisample-database"></a>Objetos de base de datos NYCTaxi_Sample

En la tabla siguiente se resume los objetos creados en la base de datos de demostración de taxis de Nueva York. Aunque solo ejecutar un script de PowerShell (`RunSQL_SQL_Walkthrough.ps1`), ese script llama a otros scripts SQL para crear los objetos en la base de datos. Los scripts usados para crear cada objeto se mencionan en la descripción.

|**Nombre de objeto**|**Tipo de objeto**|**Descripción**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | Base de datos |Crea el script create db tb carga data.sql. Crea una base de datos y dos tablas:<br /><br />tabla dbo.nyctaxi_sample: contiene el conjunto de datos NYC Taxi principal. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. El ejemplo de 1% del conjunto de datos NYC Taxi se insertará en esta tabla.<br /><br />tabla dbo.nyc_taxi_models: usa para conservar el modelo de análisis avanzado entrenado.|
|**fnCalculateDistance** |función escalar | Crea el script fnCalculateDistance.sql. Calcula la distancia directa entre las ubicaciones de recogida y destino. Esta función se utiliza en [crear características de datos](sqldev-create-data-features-using-t-sql.md), [entrenar y guardar un modelo](../r/sqldev-train-and-save-a-model-using-t-sql.md) y [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**fnEngineerFeatures** |función con valores de tabla | Crea el script fnEngineerFeatures.sql. Crea nuevas características de datos de entrenamiento del modelo. Esta función se utiliza en [crear características de datos](sqldev-create-data-features-using-t-sql.md) y [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**PlotHistogram** |procedimiento almacenado | Crea el script PlotHistogram.sql. Llama a una función de R para trazar el histograma de una variable y, a continuación, devuelve el gráfico como un objeto binario. Este procedimiento almacenado se usa en [explorar y visualizar datos](sqldev-explore-and-visualize-the-data.md).|
|**PlotInOutputFiles** |procedimiento almacenado| Crea el script PlotInOutputFiles.sql. Crea un gráfico mediante una función de R y, a continuación, guarde el resultado como un archivo PDF local. Este procedimiento almacenado se usa en [explorar y visualizar datos](sqldev-explore-and-visualize-the-data.md).|
|**PersistModel** |procedimiento almacenado | Crea el script PersistModel.sql. Toma un modelo que se ha serializado en un tipo de datos varbinary y lo escribe en la tabla especificada. |
|**PredictTip**  |procedimiento almacenado |Crea el script PredictTip.sql. Llama al modelo entrenado para crear predicciones usando el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada. Este procedimiento almacenado se usa en [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**PredictTipSingleMode**  |procedimiento almacenado| Crea el script PredictTipSingleMode.sql. Llama al modelo entrenado para crear predicciones usando el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación. Este procedimiento almacenado se usa en [Operacionalizar el modelo de R](sqldev-operationalize-the-model.md).|
|**TrainTipPredictionModel**  |procedimiento almacenado|Crea el script TrainTipPredictionModel.sql. Entrena un modelo de regresión logística mediante una llamada a un paquete de R. El modelo predice el valor de la columna tipped y se entrena usando un 70 % de los datos seleccionados aleatoriamente. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models. Este procedimiento almacenado se usa en [entrenar y guardar un modelo](../r/sqldev-train-and-save-a-model-using-t-sql.md).|

## <a name="query-data-for-verification"></a>Consultar los datos para la comprobación

Como paso de validación, ejecute una consulta para confirmar que se han cargado los datos.

1. En el Explorador de objetos, en las bases de datos, expanda el **NYCTaxi_Sample** base de datos y, a continuación, abra la carpeta tablas.

2. Haga clic en el **dbo.nyctaxi_sample** y elija **seleccionar 1000 filas superiores** devuelva datos.

## <a name="next-steps"></a>Pasos siguientes

Datos de ejemplo de taxis de Nueva York ahora están disponibles para el aprendizaje práctico.

+ [Obtenga información sobre los análisis en bases de datos con R en SQL Server](sqldev-in-database-r-for-sql-developers.md)