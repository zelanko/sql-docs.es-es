---
title: 'Lección 1 explorar y visualizar datos mediante Python y T-SQL: SQL Server Machine Learning'
description: Tutorial que muestra cómo incrustar Python en SQL Server los procedimientos almacenados y funciones de Transact-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e9dd0a0884c96a8f5b17948c21b7f891a2e997ab
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860496"
---
# <a name="explore-and-visualize-the-data"></a>Explorar y visualizar los datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial, [análisis de Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, explorar los datos de ejemplo y generará algunos trazados. Más adelante, obtendrá información sobre cómo serializar gráficos de objetos en Python y, a continuación, deserializar los objetos y hacer los trazados.

## <a name="review-the-data"></a>Revise los datos

En primer lugar, tómese un minuto para examinar el esquema de datos, como hemos hecho algunos cambios para que sea más fácil usar los datos de taxis de Nueva York

+ El conjunto de datos original utiliza archivos independientes para los identificadores de taxis y los registros de ida y vuelta. Nos hemos unido los dos conjuntos de datos originales en las columnas _medallion_, _hack_license_, y _pickup_datetime_.  
+ El conjunto de datos original abarca muchos archivos y era bastante grande. Hemos downsampled para obtener solo un 1% del número de registros original. La tabla de datos actual tiene 1 703 957 filas y 23 columnas.

**Identificadores de taxis**

El _medallion_ columna representa el número de identificación único del taxi.

El _hack_license_ columna contiene el número de licencia del conductor del taxi (anónimo).

**Registros de viajes y tarifas**

Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.

Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.

Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático.  La columna _tip_amount_ contiene valores numéricos continuos y se puede usar como la columna **label** para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. La columna _tip_class_ tiene varias **etiquetas de clase** y, por tanto, se puede usar como etiqueta para tareas de clasificación de varias clases.

Los valores utilizados para las columnas de etiqueta se basan en la `tip_amount` columna, utilizando estas reglas de negocios:

+ Columna de etiqueta `tipped` tiene posibles valores 0 y 1

    Si `tip_amount` > 0, `tipped` = 1; en caso contrario `tipped` = 0

+ Columna de etiqueta `tip_class` tiene valores de la clase posible 0-4

    Clase 0: `tip_amount` = 0 $

    Clase 1: `tip_amount` > $0 y `tip_amount` < = 5 $
    
    Clase 2: `tip_amount` > $5 y `tip_amount` < = 10 $
    
    Clase 3: `tip_amount` > $10 y `tip_amount` < = 20 $
    
    Clase 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Crear trazados con Python en T-SQL

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Porque la visualización es una herramienta eficaz para comprender la distribución de los datos y los valores atípicos, Python proporciona muchos paquetes para visualizar datos. El **matplotlib** módulo es una de las bibliotecas más populares para la visualización e incluye muchas funciones para crear histogramas, gráficos de dispersión, caja y otros gráficos de exploración de datos.

En esta sección, obtendrá información sobre cómo trabajar con trazados con procedimientos almacenados. En lugar de abrir la imagen en el servidor, almacena el objeto de Python `plot` como **varbinary** datos y después escribir que en un archivo que puede compartir o visualizarse en otro lugar.

### <a name="create-a-plot-as-varbinary-data"></a>Crear un gráfico como datos varbinary

El procedimiento almacenado devuelve un número de serie de Python `figure` objeto como un flujo de **varbinary** datos. No se puede ver los datos binarios directamente, pero puede usar código de Python en el cliente para deserializar y ver las cifras y, a continuación, guarde el archivo de imagen en un equipo cliente.

1. Crear el procedimiento almacenado **PyPlotMatplotlib**, si el script de PowerShell ya no lo hizo.

    - La variable `@query` define el texto de consulta `SELECT tipped FROM nyctaxi_sample`, que se pasa al bloque de código Python como el argumento de la variable de entrada de secuencia de comandos, `@input_data_1`.
    - El script de Python es bastante simple: **matplotlib** `figure` objetos sirven para hacer que el trazado de dispersión y de histograma, y estos objetos se serializan utilizando la `pickle` biblioteca.
    - El objeto de gráficos de Python se serializa a un **pandas** trama de datos de salida.
  
    ```sql
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
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

2. Ahora puede ejecutar el procedimiento almacenado sin argumentos para generar un trazado de los datos codificados de forma rígida como consulta de entrada.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. Los resultados deben ser algo parecido a esto:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Desde un [cliente Python](../python/setup-python-client-tools-sql.md), ahora puede conectarse a la instancia de SQL Server que generan los objetos de trazado binario y ver los trazados. 

    Para ello, ejecute el siguiente código de Python, reemplazando el nombre del servidor, nombre de base de datos y las credenciales según corresponda. Asegúrese de que la versión de Python es el mismo en el cliente y el servidor. Además, asegúrese de que las bibliotecas de Python en el cliente (como matplotlib) son la versión igual o superior en relación con las bibliotecas instaladas en el servidor.
  
    **Mediante la autenticación de SQL Server:**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **Mediante la autenticación de Windows:**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  Si la conexión se realiza correctamente, debería ver un mensaje similar al siguiente:
  
    *Los trazados se guardan en el directorio: xxxx*
  
6.  El archivo de salida se crea en el directorio de trabajo de Python. Para ver el trazado, busque el directorio de trabajo de Python y abra el archivo. La siguiente imagen muestra un gráfico que se guardan en el equipo cliente.
  
    ![Sugerencia de importe de cantidad vs](media/sqldev-python-sample-plot.png "importe de vs de cantidad de sugerencia") 

## <a name="next-step"></a>Paso siguiente

[Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Paso anterior

[Descargue el conjunto de datos de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)

