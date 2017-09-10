---
title: 'Paso 2: Importar datos a SQL Server mediante PowerShell | Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-vnext-ctp2
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62a06d6c442428132f84b3f8e5a665e872a8d361
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>Paso 2: Importar datos a SQL Server mediante PowerShell

En este paso, ejecutará uno de los scripts descargados para crear los objetos de base de datos necesarios para el tutorial. El script también crea la mayoría de los procedimientos almacenados que va a usar y carga los datos de ejemplo en una tabla de la base de datos especificada.

## <a name="create-sql-objects-and-data"></a>Crear objetos de SQL y de datos

Entre los archivos descargados, verá un script de PowerShell. Para preparar el entorno para el tutorial, deberá ejecutar este script.  El script realiza estas acciones:

- Instala el cliente nativo de SQL y utilidades de línea de comandos de SQL, si aún no está instalado. Estas utilidades son necesarias para la carga masiva de los datos en la mediante **bcp**.

- Crea una base de datos y una tabla en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia e inserciones masivas de datos en la tabla.

- Crea varios procedimientos almacenados y funciones SQL.

### <a name="run-the-script"></a>Ejecute la secuencia de comandos

1. Abra un símbolo del sistema de PowerShell como administrador y ejecute el siguiente comando.
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  

    Se le pedirá que escriba la siguiente información:
    - El nombre o la dirección de un [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instancia donde se ha instalado los servicios con Python de aprendizaje automático
    - El nombre de usuario y la contraseña de una cuenta en la instancia. La cuenta que use debe tener la capacidad de crear bases de datos, crear tablas y procedimientos almacenados, y cargar datos en tablas. Si no se proporciona el nombre de usuario y la contraseña, la identidad de Windows se utiliza para iniciar sesión en SQL Server.
    - La ruta de acceso y el nombre de archivo del archivo de datos de ejemplo que acaba de descargar. Por ejemplo, `C:\tempRSQL\nyctaxi1pct.csv`

    > [!NOTE]
    > Asegúrese de que su xmlrw.dll está en la misma carpeta que su bcp.exe. Si no es así, cópielo en.

2.  Como parte de este paso, todos los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] también se modifican para reemplazar los marcadores de posición con el nombre de la base de datos y el nombre de usuario que proporcionó como entradas de script.
  
3. Tómese un minuto para revisar los procedimientos almacenados y las funciones creadas por el script.
     
    |**Nombre de archivo del script de SQL**|**Función**|
    |------|------|
    |create-db-tb-upload-data.sql|Crea una base de datos y dos tablas:<br /><br />nyctaxi_sample: contiene el conjunto de datos NYC Taxi principal. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta. La muestra del 1 % del conjunto de datos NYC Taxi se insertará en esta tabla.<br /><br />nyc_taxi_models: se usa para conservar el modelo de análisis avanzado entrenado.|
    |fnCalculateDistance.sql|Crea una función con valores escalares que calcula la distancia directa entre las ubicaciones de origen y destino.|
    |fnEngineerFeatures.sql|Crea una función con valores de tabla que crea nuevas características de datos para el entrenamiento del modelo.|
    |TrainingTestingSplit.sql|Dividir los datos en la tabla nyctaxi_sample en dos partes: nyctaxi_sample_training y nyctaxi_sample_testing.|
    |PredictTipSciKitPy.sql|Crea un procedimiento almacenado que llama al modelo entrenado (scikit-aprender) para crear predicciones mediante el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada.|
    |PredictTipRxPy.sql|Crea un procedimiento almacenado que llama al modelo entrenado (revoscalepy) para crear predicciones utilizando el modelo. El procedimiento almacenado acepta una consulta como su parámetro de entrada y devuelve una columna de valores numéricos que contiene los resultados para las filas de entrada.|
    |PredictTipSingleModeSciKitPy.sql|Crea un procedimiento almacenado que llama al modelo entrenado (scikit-aprender) para crear predicciones mediante el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación.|
    |PredictTipSingleModeRxPy.sql|Crea un procedimiento almacenado que llama al modelo entrenado (revoscalepy) para crear predicciones utilizando el modelo. Este procedimiento almacenado acepta una observación nueva como entrada, con valores de características individuales pasados como parámetros en línea, y devuelve un valor que predice el resultado de la nueva observación.|
  
4. En la última parte de este tutorial, creará algunos procedimientos almacenados adicionales:
    
    |**Nombre de archivo del script de SQL**|**Función**|
    |------|------|
    |SerializePlots.sql|Crea un procedimiento almacenado para la exploración de datos. Este procedimiento almacenado crea un gráfico con Python y, a continuación, serializar los objetos del gráfico.|
    |TrainTipPredictionModelSciKitPy.sql|Crea un procedimiento almacenado que entrena un modelo de regresión logística (scikit-Obtenga información acerca de). El modelo predice el valor de la columna superpuesto y se entrena usando un seleccionado aleatoriamente del 60% de los datos. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models.|
    |TrainTipPredictionModelRxPy.sql|Crea un procedimiento almacenado que entrena un modelo de regresión logística (revoscalepy). El modelo predice el valor de la columna superpuesto y se entrena usando un seleccionado aleatoriamente del 60% de los datos. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models.|
  
3. Inicie sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y el inicio de sesión especificado, para comprobar que puede ver la base de datos, las tablas, funciones y procedimientos almacenados que se crearon.

    ![Examinar tablas en SSMS](media/sqldev-python-browsetables1.png "ver tablas en SSMS")

    > [!NOTE]
    > Si los objetos de base de datos ya existen, no se pueden crear de nuevo. Si la tabla ya existe, los datos se anexarán, no se sobrescriben. Por tanto, asegúrese de quitar todos los objetos existentes antes de ejecutar el script.
    > Siga las instrucciones [aquí](https://docs.microsoft.com/en-us/sql/advanced-analytics/r/set-up-sql-server-r-services-in-database#bkmk_enableFeature) para habilitar los servicios de script externo.
    


## <a name="next-step"></a>Paso siguiente

[Paso 3: Explorar y visualizar los datos](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>Paso anterior

[Paso 1: Descargar los datos de ejemplo](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)



