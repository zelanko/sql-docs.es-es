---
title: Lección 1 explorar y visualizar datos con Python y T-SQL
description: Tutorial que muestra cómo insertar Python en SQL Server procedimientos almacenados y funciones de T-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0442fd942f0dd509f24b98b5ca1c6d6c31a197f0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470555"
---
# <a name="explore-and-visualize-the-data"></a>Explore y visualice los datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo forma parte de un tutorial, [análisis de Python en base de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md). 

En este paso, explorará los datos de ejemplo y generará algunos trazados. Más adelante, aprenderá a serializar objetos gráficos en Python y, a continuación, deserializar esos objetos y crear trazados.

## <a name="review-the-data"></a>Revisar los datos

En primer lugar, dedique un minuto a examinar el esquema de datos, ya que hemos realizado algunos cambios para facilitar el uso de los datos de taxi de Nueva York.

+ El conjunto de documentos original usaba archivos independientes para los identificadores de taxi y los registros de viaje. Hemos unido los dos conjuntos de valores originales en las columnas _Medallion_, _hack_license_y _pickup_datetime_.  
+ El conjunto de filas original abarca muchos archivos y era bastante grande. Se Downsampled para obtener solo un 1% del número original de registros. La tabla de datos actual tiene 1.703.957 filas y 23 columnas.

**Identificadores de taxis**

La columna _Medallion_ representa el número de identificación único del taxi.

La columna _hack_license_ contiene el número de licencia del controlador de taxi (anónimos).

**Registros de viajes y tarifas**

Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.

Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.

Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático.  La columna _tip_amount_ contiene valores numéricos continuos y se puede usar como la columna **label** para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. La columna _tip_class_ tiene varias **etiquetas de clase** y, por tanto, se puede usar como etiqueta para tareas de clasificación de varias clases.

Los valores utilizados para las columnas de etiqueta se basan en la `tip_amount` columna, mediante estas reglas de negocios:

+ La columna `tipped` de etiqueta tiene los valores posibles 0 y 1

    Si `tip_amount` > 0, `tipped` = 1; en `tipped` caso contrario = 0

+ La columna `tip_class` de etiqueta tiene valores de clase posibles 0-4

    Clase 0: `tip_amount` = $0

    Clase 1: `tip_amount` > $0 y `tip_amount` < = $5
    
    Clase 2: `tip_amount` > $5 y `tip_amount` < = $10
    
    Clase 3: `tip_amount` > $10 y `tip_amount` < = $20
    
    Clase 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>Creación de trazados con Python en T-SQL

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Dado que la visualización es una herramienta muy eficaz para comprender la distribución de los datos y los valores atípicos, Python proporciona muchos paquetes para visualizar los datos. El módulo **matplotlib** es una de las bibliotecas más populares para la visualización e incluye muchas funciones para crear histogramas, gráficos de dispersión, gráficos de cuadros y otros gráficos de exploración de datos.

En esta sección, aprenderá a trabajar con trazados mediante procedimientos almacenados. En lugar de abrir la imagen en el servidor, se almacena el objeto `plot` Python como datos **varbinary** y, a continuación, se escribe en un archivo que se puede compartir o ver en otro lugar.

### <a name="create-a-plot-as-varbinary-data"></a>Crear un trazado como datos varbinary

El procedimiento almacenado devuelve un objeto de Python `figure` serializado como un flujo de datos **varbinary** . No puede ver los datos binarios directamente, pero puede usar el código de Python en el cliente para deserializar y ver las cifras y, a continuación, guardar el archivo de imagen en un equipo cliente.

1. Cree el procedimiento almacenado **PyPlotMatplotlib**, si el script de PowerShell no lo ha hecho todavía.

    - La variable `@query` define el texto `SELECT tipped FROM nyctaxi_sample`de la consulta, que se pasa al bloque de código de Python como el argumento a la variable `@input_data_1`de entrada de script,.
    - El script de Python es bastante sencillo: los objetos **matplotlib** `figure` se usan para crear el histograma y el gráfico de dispersión, y estos objetos se serializan a continuación mediante la `pickle` biblioteca.
    - El objeto de gráficos de Python se serializa en una trama de **pandas** para la salida.
  
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

2. Ahora, ejecute el procedimiento almacenado sin argumentos para generar un trazado a partir de los datos codificados de forma rígida como consulta de entrada.

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. Los resultados deben ser similares a los siguientes:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. Desde un [cliente de Python](../python/setup-python-client-tools-sql.md), ahora puede conectarse a la instancia de SQL Server que generó los objetos de trazado binario y ver los trazados. 

    Para ello, ejecute el siguiente código de Python, reemplazando el nombre del servidor, el nombre de la base de datos y las credenciales según corresponda. Asegúrese de que la versión de Python es la misma en el cliente y en el servidor. Asegúrese también de que las bibliotecas de Python en el cliente (por ejemplo, matplotlib) son la misma versión o una superior relativa a las bibliotecas instaladas en el servidor.
  
    **Usar la autenticación de SQL Server:**
    
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

    **Usar la autenticación de Windows:**

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

5.  Si la conexión es correcta, debería ver un mensaje similar al siguiente:
  
    *Los trazados se guardan en el directorio: xxxx*
  
6.  El archivo de salida se crea en el directorio de trabajo de Python. Para ver el trazado, busque el directorio de trabajo de Python y abra el archivo. La siguiente imagen muestra un trazado guardado en el equipo cliente.
  
    ![Importe de propinas frente a importe de tarifa](media/sqldev-python-sample-plot.png "Importe de propinas frente a importe de tarifa") 

## <a name="next-step"></a>Paso siguiente

[Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Paso anterior

[Descarga del conjunto de datos de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)

