---
title: Paso 2 importar datos a SQL Server mediante PowerShell | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 14606b42d17acdd56527795d2d475a263d918d7d
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2018
ms.locfileid: "35249998"
---
# <a name="step-2-import-data-to-sql-server-using-powershell"></a>Paso 2: Importar datos a SQL Server usando PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, ejecute uno de los scripts descargados para crear los objetos de base de datos necesarios para el tutorial. El script también crea varios procedimientos almacenados y carga los datos de ejemplo en una tabla en la base de datos especificada.

## <a name="create-database-objects-and-load-data"></a>Crear objetos de base de datos y cargar datos

Entre los archivos descargados debería ver un script de PowerShell, `RunSQL_SQL_Walkthrough.ps1`. El propósito de este script es preparar el entorno para el tutorial.

El script realiza estas acciones:

- Instala el cliente nativo de SQL y utilidades de línea de comandos de SQL, si aún no está instalado. Estas utilidades son necesarias para la carga masiva de los datos en la mediante **bcp**.

- Crea una base de datos y una tabla en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia e inserciones masivas de datos en la tabla.

- Crea varios procedimientos almacenados y funciones SQL.

Si experimenta problemas, puede usar la secuencia de comandos como una referencia para realizar los pasos manualmente.

### <a name="modify-the-script-to-use-a-trusted-windows-identity"></a>Modifique el script para usar una identidad de Windows de confianza

De forma predeterminada, el script asume que un inicio de sesión de usuario de base de datos de SQL Server y una contraseña. Si estás db_owner en su cuenta de usuario de Windows, puede usar la identidad de Windows para crear los objetos. Para ello, abra `RunSQL_SQL_Walkthrough.ps1` en un editor de código para anexar **`-T`** a bcp bulk insert, comando:

```text
bcp $db_tb in $csvfilepath -t ',' -S $server -f taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U $u -P $p -T
```

### <a name="run-the-script"></a>Ejecute la secuencia de comandos

1. Abra un símbolo del sistema de PowerShell como administrador. Si no está ya en la carpeta creada en el paso anterior, vaya a la carpeta y, a continuación, ejecute el siguiente comando:
  
    ```ps
    .\RunSQL_SQL_Walkthrough.ps1
    ```

2. La secuencia de comandos solicita la siguiente información:

    - El nombre o la dirección de un [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instancia donde se ha instalado servicios de aprendizaje de máquina con Python.
    - El nombre de usuario y la contraseña de una cuenta en la instancia. La cuenta que utilice debe tener la capacidad de crear las bases de datos, crear tablas y procedimientos almacenados y carga masiva de datos a tablas. 
    - Si no se proporciona el nombre de usuario y la contraseña, la identidad de Windows se utiliza para iniciar sesión en SQL Server.
    - La ruta de acceso y el nombre de archivo del archivo de datos de ejemplo que acaba de descargar. Por ejemplo, `C:\temp\pysql\nyctaxi1pct.csv`

    > [!NOTE]
    > Para cargar los datos correctamente, la biblioteca xmlrw.dll debe estar en la misma carpeta que bcp.exe.

3. El script también modifica el [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos que descargó anteriormente y reemplaza los marcadores de posición con el nombre de la base de datos y el usuario el nombre que se proporcionan.
  
4. Cuando se completa la secuencia de comandos, inicie sesión en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia mediante el inicio de sesión especificado, para comprobar que la base de datos, tablas, funciones y procedimientos almacenados que se han creado. La siguiente imagen muestra los objetos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

    ![Examinar tablas en SSMS](media/sqldev-python-browsetables1.png "ver tablas en SSMS")

    > [!NOTE]
    > Si los objetos de base de datos ya existían, no se puede crear nuevo.
    > 
    > Si se encuentra una tabla existente del mismo nombre y el esquema, los datos se anexarán, no se sobrescribe. Por lo tanto, asegúrese de quitar o truncar las tablas existentes antes de ejecutar la secuencia de comandos.

## <a name="list-of-stored-procedures-and-functions"></a>Lista de procedimientos almacenados y funciones

Los siguientes objetos de SQL Server se crean mediante la secuencia de comandos:

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

En la última parte de este tutorial, cree estos procedimientos almacenados adicionales:
    
|**Nombre de archivo del script de SQL**|**Función**|
|------|------|
|SerializePlots.sql|Crea un procedimiento almacenado para la exploración de datos. Este procedimiento almacenado crea un gráfico con Python y, a continuación, serializar los objetos del gráfico.|
|TrainTipPredictionModelSciKitPy.sql|Crea un procedimiento almacenado que entrena un modelo de regresión logística (scikit-Obtenga información acerca de). El modelo predice el valor de la columna superpuesto y se entrena usando un seleccionado aleatoriamente del 60% de los datos. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models.|
|TrainTipPredictionModelRxPy.sql|Crea un procedimiento almacenado que entrena un modelo de regresión logística (revoscalepy). El modelo predice el valor de la columna superpuesto y se entrena usando un seleccionado aleatoriamente del 60% de los datos. El resultado del procedimiento almacenado es el modelo entrenado, que se guarda en la tabla nyc_taxi_models.|

## <a name="next-step"></a>Paso siguiente

[Paso 3: Explorar y visualizar los datos](sqldev-py3-explore-and-visualize-the-data.md)

## <a name="previous-step"></a>Paso anterior

[Paso 1: Descargar los datos de ejemplo](sqldev-py1-download-the-sample-data.md)

