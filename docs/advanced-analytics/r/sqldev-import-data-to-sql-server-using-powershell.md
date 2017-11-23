---
title: "Lección 2: Importar datos a SQL Server mediante PowerShell | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c9190157b005158bb2ca8b9aeb7addbdbf1e69f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-2-import-data-to-sql-server-using-powershell"></a>Lección 2: Importar datos a SQL Server usando PowerShell

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, ejecutará uno de los scripts descargados para crear los objetos de base de datos necesarios para el tutorial. El script también crea la mayoría de los procedimientos almacenados que va a usar y carga los datos de ejemplo en una tabla de la base de datos especificada.

## <a name="run-the-scripts-to-create-sql-objects"></a>Ejecutar las secuencias de comandos para crear objetos SQL

Entre los archivos descargados, debería ver un script de PowerShell que se pueden ejecutar para preparar el entorno para el tutorial. Las acciones realizadas por el script son las siguientes:

- Instalación del cliente nativo de SQL y las utilidades de línea de comandos de SQL, si todavía no están instalados. Estas utilidades son necesarias para la carga masiva de los datos en la mediante **bcp**.

- Creación de una base de datos y una tabla en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inserción masiva de los datos en la tabla.

- Creación de varios procedimientos almacenados y funciones de SQL.

### <a name="run-the-script"></a>Ejecute la secuencia de comandos

1.  Abra un símbolo del sistema de PowerShell como administrador y ejecute el siguiente comando.
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```
  
    Se le pedirá que escriba la siguiente información:
  
    - El nombre o la dirección de una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] donde se haya instalado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]
  
    - El nombre de usuario y la contraseña de una cuenta en la instancia. La cuenta debe tener permisos para crear bases de datos, crear tablas y procedimientos almacenados y cargar datos en tablas. Si no se proporciona el nombre de usuario y la contraseña, la identidad de Windows se utiliza para iniciar sesión en SQL Server.
  
    - La ruta de acceso y el nombre de archivo del archivo de datos de ejemplo que acaba de descargar. Por ejemplo:
  
        `C:\tempRSQL\nyctaxi1pct.csv`
  
2.  Como parte de este paso, todos los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] también se modifican para reemplazar los marcadores de posición con el nombre de la base de datos y el nombre de usuario que proporcionó como entradas de script.
  
    Tómese un minuto para revisar los procedimientos almacenados y las funciones creadas por el script.
  
    |**Nombre de archivo del script de SQL**|**Función**|
    |-|-|
    |create-db-tb-upload-data.sql|Crea una base de datos y dos tablas:<br /><br />nyctaxi_sample: contiene el conjunto de datos NYC Taxi principal. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. La muestra del 1 % del conjunto de datos NYC Taxi se insertará en esta tabla.<br /><br />nyc_taxi_models: se usa para conservar el modelo de análisis avanzado entrenado.|
    |fnCalculateDistance.sql|Crea una función con valores escalares que calcula la distancia directa entre las ubicaciones de origen y destino.|
    |fnEngineerFeatures.sql|Crea una función con valores de tabla que crea nuevas características de datos para el entrenamiento del modelo.|
    |PersistModel.sql|Crea un procedimiento almacenado que se puede llamar para guardar un modelo. El procedimiento almacenado toma un modelo que se ha serializado en un tipo de datos varbinary y lo escribe en la tabla especificada.|
    |PredictTipBatchMode.sql|Crea un procedimiento almacenado que llama al modelo entrenado para crear predicciones usando el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada.|
    |PredictTipSingleMode.sql|Crea un procedimiento almacenado que llama al modelo entrenado para crear predicciones usando el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación.|
  
    En la última parte de este tutorial, creará algunos procedimientos almacenados adicionales:
  
    |**Nombre de archivo del script de SQL**|**Función**|
    |------|------|
    |PlotHistogram.sql|Crea un procedimiento almacenado para la exploración de datos. Este procedimiento almacenado llama a una función de R para trazar el histograma de una variable y, después, devuelve el gráfico como un objeto binario.|
    |PlotInOutputFiles.sql|Crea un procedimiento almacenado para la exploración de datos. Este procedimiento almacenado crea un gráfico mediante una función de R y, después, guarda el resultado como un archivo PDF local.|
    |TrainTipPredictionModel.sql|Crea un procedimiento almacenado que entrena un modelo de regresión logística mediante una llamada a un paquete de R. El modelo predice el valor de la columna tipped y se entrena usando un 70 % de los datos seleccionados aleatoriamente. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models.|
  
3.  Inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el inicio de sesión especificado, para comprobar que puede ver la base de datos, las tablas, funciones y procedimientos almacenados que se crearon.
  
    ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")
  
    > [!NOTE]
    > Si los objetos de base de datos ya existen, no se pueden crear de nuevo.
    >   
    > Si la tabla ya existe, los datos se anexarán, no se sobrescriben. Por tanto, asegúrese de quitar todos los objetos existentes antes de ejecutar el script.

## <a name="next-lesson"></a>Lección siguiente

[Lección 3: Explorar y visualizar los datos](../tutorials/sqldev-explore-and-visualize-the-data.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 1: Descargar los datos de ejemplo](../tutorials/sqldev-download-the-sample-data.md)
