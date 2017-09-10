---
title: 'Paso 3: Explorar y visualizar los datos| Microsoft Docs'
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-python
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
ms.openlocfilehash: dfb80fcd3241b22f0ac72c2cf4cd8a18d1add857
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>Paso 3: Explorar y visualizar los datos

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. En este paso, podrá explorar los datos de ejemplo y generar algunos gráficos. Más adelante, obtendrá información sobre cómo serializar gráficos de objetos de Python y, a continuación, deserializar los objetos y hacer trazados.

> [!NOTE]
> Este tutorial muestra la tarea de clasificación binaria; son bienvenida pruebe a generar modelos independientes para las otras tareas de aprendizaje automático de dos, la regresión y clasificación multiclase.

## <a name="review-the-data"></a>Revisar los datos

En el conjunto de datos original, los identificadores de taxis y los registros de viaje se proporcionaron en archivos independientes. En cambio, para facilitar el uso de los datos de ejemplo, los dos conjuntos de datos originales se han unido en las columnas _medallion_, _hack_license_y _pickup_datetime_.  Los registros también se muestrearon para obtener solo un 1 % del número de registros original. El conjunto de datos muestreado resultante tiene 1 703 957 filas y 23 columnas.

**Identificadores de taxis**

- La columna _medallion_ representa el número de identificador único del taxi.
- La columna _hack_license_ contiene el número de licencia del conductor del taxi (anónimo).

**Registros de viajes y tarifas**

- Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.
- Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.
- Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático.  La columna _tip_amount_ contiene valores numéricos continuos y se puede usar como la columna **label** para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. La columna _tip_class_ tiene varias **etiquetas de clase** y, por tanto, se puede usar como etiqueta para tareas de clasificación de varias clases.
- Los valores usados para las columnas de etiqueta se basan en la columna _tip_amount_ , usando estas reglas de negocios:
  
    |Nombre de columna derivada|Regla|
    |-|-|
     |tipped|Si tip_amount > 0, tipped = 1, de lo contrario, tipped = 0|
    |tip_class|Clase 0: tip_amount = 0 $<br /><br />Clase 1: tip_amount > 0 $ y tip_amount < = 5 $<br /><br />Clase 2: tip_amount > 5 $ y tip_amount < = 10 $<br /><br />Clase 3: tip_amount > 10 $ y tip_amount < = 20 $<br /><br />Clase 4: tip_amount > 20 $|

## <a name="create-plots-using-python-in-t-sql"></a>Crear gráficos con Python en T-SQL

Dado que visualización es una herramienta eficaz para comprender la distribución de los datos y los valores atípicos, Python proporciona varios paquetes para la visualización de datos. El **matplotlib** módulo es una biblioteca popular que incluye muchas funciones para crear histogramas, los gráficos de dispersión, cuadro gráficos y otros gráficos de exploración de datos.

En esta sección, aprenderá cómo trabajar con gráficos de uso de procedimientos almacenados. Va a almacenar el `plot` Python objeto como un **varbinary** datos escribir y guardar los gráficos generados en el servidor.

### <a name="storing-plots-as-varbinary-data-type"></a>Almacenar trazados como tipo de datos varbinary

El **revoscalepy** módulo incluido con SQL Server de 2017 Machine Learning Services contiene bibliotecas análogas a las bibliotecas de R en el paquete RevoScaleR. En este ejemplo, usarás el equivalente de Python de `rxHistogram` para trazar un histograma en función de los datos de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Para facilitar la tarea, se encapsulará en un procedimiento almacenado, _PlotHistogram_.

El procedimiento almacenado devuelve un número de serie de Python `figure` objeto como un flujo de **varbinary** datos. No se puede ver los datos binarios directamente, pero puede utilizar código de Python en el cliente para deserializar y ver las cifras y, a continuación, guarde el archivo de imagen en un equipo cliente.

### <a name="create-the-stored-procedure-plotspython"></a>Crear el procedimiento almacenado Plots_Python

1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una nueva **consulta** ventana.

2.  Seleccione la base de datos para el tutorial y cree el procedimiento con esta instrucción. Asegúrese de modificar el código para usar el nombre de tabla correcto, si es necesario.
  
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
**Comentarios:**

- La variable `@query` define el texto de consulta (`'SELECT tipped FROM nyctaxi_sample'`), que se pasa al bloque de código Python como argumento para la variable de entrada de secuencia de comandos, `@input_data_1`.
- El script de Python es bastante sencillo: **matplotlib** `figure` objetos se usan para hacer el gráfico de dispersión y de histograma, y estos objetos, a continuación, se serializan con la `pickle` biblioteca.
- El objeto de gráfico de Python se serializa a un Python **pandas** trama de datos de salida.

### <a name="output-varbinary-data-to-viewable-graphics-file"></a>Datos varbinary de salida al archivo de gráficos visibles

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la instrucción siguiente:
  
    ```
    EXEC [dbo].[SerializePlots]
    ```
  
    **Resultado**
  
    *gráfico de*
    *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649... * 
     *0xFFD8FFE000104A4649...*

  
2.  En el equipo cliente, ejecute el siguiente código de Python, reemplazando el nombre del servidor, nombre de base de datos y las credenciales según corresponda.
  
    **Para la autenticación de SQL server:**
    
        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSOWRD}')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```  
    **Para la autenticación de Windows:**

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

    > [!NOTE]
    > Asegúrese de que la versión de Python es el mismo en el cliente y el servidor. Además, asegúrese de que las bibliotecas de Python que está usando en el cliente (por ejemplo, matplotlib) son de la versión igual o mayor en relación con las bibliotecas instaladas en el servidor.


3.  Si la conexión se realiza correctamente, verá los resultados siguientes
  
    *Los gráficos se guardan en el directorio: xxxx*
  
4.  El archivo de salida se creará en el directorio de trabajo de Python. Para ver el gráfico, abra el directorio de trabajo de Python. La siguiente imagen muestra un gráfico en el ejemplo se guardan en el equipo cliente.
  
    ![Sugerencia de cantidad de tarifa de vs cantidad](media/sqldev-python-sample-plot.png "cantidad de tarifa de vs de cantidad de sugerencia") 

## <a name="next-step"></a>Paso siguiente

[Paso 4: Crear características de datos mediante T-SQL](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>Paso anterior

[Paso 2: Importar datos a SQL Server mediante PowerShell](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="see-also"></a>Vea también

[Los servicios con Python de aprendizaje automático](../python/sql-server-python-services.md)

