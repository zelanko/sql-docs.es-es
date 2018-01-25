---
title: 'Paso 3: Explorar y visualizar los datos | Documentos de Microsoft'
ms.custom: 
ms.date: 10/17/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: "2"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 773566697840473bc9e22b55452980b21a308ebc
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="step-3-explore-and-visualize-the-data"></a>Paso 3: Explorar y visualizar los datos

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, explorar los datos de ejemplo y generar algunos gráficos. Más adelante, se muestra cómo serializar gráficos de objetos de Python y, a continuación, deserializar los objetos y hacer trazados.

## <a name="review-the-data"></a>Revise los datos

En primer lugar, tómese un minuto para examinar el esquema de datos, tal y como hemos realizado algunos cambios para que resulten más fáciles de usar los datos de Nueva York Taxi

+ El conjunto de datos original utiliza archivos independientes para los identificadores de taxi y los registros de ida y vuelta. Nos hemos combinadas los dos conjuntos de datos originales en las columnas _medallion_, _hack_license_, y _pickup_datetime_.  
+ El conjunto de datos original que abarca todos los archivos y es bastante grande. Hemos reduce para obtener solo el 1% del número de registros original. La tabla de datos actual tiene 1,703,957 filas y 23 columnas.

**Identificadores de taxis**

El _medallion_ columna representa el número de identificación único del taxi.

El _hack_license_ columna contiene el número de licencia del controlador taxi (anónimos).

**Registros de viajes y tarifas**

Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.

Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.

Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático.  La columna _tip_amount_ contiene valores numéricos continuos y se puede usar como la columna **label** para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. La columna _tip_class_ tiene varias **etiquetas de clase** y, por tanto, se puede usar como etiqueta para tareas de clasificación de varias clases.

Los valores utilizados para las columnas de etiqueta se basan en la `tip_amount` columna, utilizando estas reglas de negocios:

+ Columna de etiqueta `tipped` tiene posibles valores 0 y 1

    Si `tip_amount` > 0, `tipped` = 1; en caso contrario `tipped` = 0

+ Columna de etiqueta `tip_class` tiene clase posibles valores de 0 a 4

    Clase 0: `tip_amount` = $0

    Clase 1: `tip_amount` > $0 y `tip_amount` < = $5
    
    Clase 2: `tip_amount` > $5 y `tip_amount` < = 10 $
    
    Clase 3: `tip_amount` > $10 y `tip_amount` < = 20 $
    
    Clase 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Crear gráficos con Python en T-SQL

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Dado que visualización es una herramienta eficaz para comprender la distribución de los datos y los valores atípicos, Python proporciona varios paquetes para la visualización de datos. El **matplotlib** módulo es una de las bibliotecas más populares para la visualización e incluye muchas funciones para crear histogramas, los gráficos de dispersión, cuadro gráficos y otros gráficos de exploración de datos.

En esta sección, aprenderá a trabajar con gráficos de uso de procedimientos almacenados. En su lugar de abrir la imagen en el servidor, almacena el objeto de Python `plot` como **varbinary** datos y después escribir que en un archivo que puede compartir o visualizarse en otro lugar.

### <a name="create-a-plot-as-varbinary-data"></a>Crear un gráfico como datos varbinary

El **revoscalepy** módulo incluido con SQL Server de 2017 Machine Learning Services admite características parecidas a las de la **RevoScaleR** paquete de R.  Este ejemplo utiliza el equivalente de Python de `rxHistogram` para trazar un histograma en función de los datos de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. 

El procedimiento almacenado devuelve un número de serie de Python `figure` objeto como un flujo de **varbinary** datos. No se puede ver los datos binarios directamente, pero puede utilizar código de Python en el cliente para deserializar y ver las cifras y, a continuación, guarde el archivo de imagen en un equipo cliente.

1. Crear el procedimiento almacenado _SerializePlots_, si la secuencia de comandos de PowerShell ya no lo hizo.

    - La variable `@query` define el texto de consulta `SELECT tipped FROM nyctaxi_sample`, que se pasa al bloque de código Python como argumento para la variable de entrada de secuencia de comandos, `@input_data_1`.
    - El script de Python es bastante sencillo: **matplotlib** `figure` objetos se usan para hacer el gráfico de dispersión y de histograma, y estos objetos, a continuación, se serializan con la `pickle` biblioteca.
    - El objeto de gráfico de Python se serializa a un **pandas** trama de datos de salida.
  
    ```SQL
    CREATE PROCEDURE [dbo].[SerializePlots]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
      EXECUTE sp_execute_external_script
      @language = N'Python',
      @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. Ahora puede ejecutar el procedimiento almacenado sin argumentos para generar un gráfico de los datos codificados de forma rígida como consulta de entrada.

    ```
    EXEC [dbo].[SerializePlots]
    ```

3. Los resultados deben ser algo parecido a esto:
  
    ```
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Desde un cliente de Python, ahora puede conectarse a la instancia de SQL Server que generan los objetos de trazado binario y ver los gráficos. 

    Para ello, ejecute el siguiente código de Python, reemplazando el nombre del servidor, nombre de base de datos y las credenciales según corresponda. Asegúrese de que la versión de Python es el mismo en el cliente y el servidor. Además, asegúrese de que las bibliotecas de Python en el cliente (por ejemplo, matplotlib) tienen la versión igual o mayor en relación con las bibliotecas instaladas en el servidor.
  
    **Mediante la autenticación de SQL Server:**
    
    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Mediante la autenticación de Windows:**

    ```python
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=yes;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[SerializePlots]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  Si la conexión se realiza correctamente, verá un mensaje similar al siguiente:
  
    *Los gráficos se guardan en el directorio: xxxx*
  
6.  El archivo de salida se crea en el directorio de trabajo de Python. Para ver el trazado, busque el directorio de trabajo de Python y abra el archivo. La siguiente imagen muestra un gráfico que se guardan en el equipo cliente.
  
    ![Sugerencia de cantidad de tarifa de vs cantidad](media/sqldev-python-sample-plot.png "cantidad de tarifa de vs de cantidad de sugerencia") 

## <a name="next-step"></a>Paso siguiente

[Paso 4: Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Paso anterior

[Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

