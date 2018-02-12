---
title: "Lección 3: Explorar y visualizar los datos | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 7d0d272c2623d2a23a8e486f15c320d40cba6bf5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>Lección 3: Explorar y visualizar los datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En esta lección, podrá revisar los datos de ejemplo y, a continuación, generar algunos gráficos de uso de funciones de R. Estas funciones de R ya están incluidas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Puede llamar a las funciones de R desde [!INCLUDE[tsql](../../includes/tsql-md.md)].

## <a name="review-the-data"></a>Revise los datos

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Por lo que primero dedique un minuto a revisar los datos de ejemplo, si no lo ha hecho ya.

En el conjunto de datos original, los identificadores de taxis y los registros de viaje se proporcionaron en archivos independientes. Sin embargo, para hacer más fácil de usar los datos de ejemplo, los dos conjuntos de datos originales se han unido en las columnas _medallion_, _hack\_licencia_, y _recogida\_ fecha y hora_.  Los registros también se muestrearon para obtener solo un 1 % del número de registros original. El conjunto de datos muestreado resultante tiene 1 703 957 filas y 23 columnas.

**Identificadores de taxis**
  
-   La columna _medallion_ representa el número de identificador único del taxi.
  
-   El _hack\_licencia_ columna contiene el número de licencia del controlador taxi (anónimos).
  
**Registros de viajes y tarifas**
  
-   Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.
  
-   Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.
  
-   Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático.  El _sugerencia\_cantidad_ columna contiene valores numéricos continuos y se pueden usar como el **etiqueta** columna para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. El _sugerencia\_clase_ columna tiene varios **clase etiquetas** y, por tanto, se puede utilizar como la etiqueta para las tareas de clasificación multiclase.
  
    Este tutorial muestra solo la tarea de clasificación binaria; puede intentar crear modelos de las otras dos tareas de aprendizaje automático, regresión y clasificación de varias clases.
  
-   Los valores utilizados para las columnas de etiqueta se basan en el _sugerencia\_cantidad_ columna, utilizando estas reglas de negocios:
  
    |Nombre de columna derivada|Regla|
    |-|-|
     |tipped|Si tip_amount > 0, tipped = 1, de lo contrario, tipped = 0|
    |tip_class|Clase 0: tip_amount = 0 $<br /><br />Clase 1: tip_amount > 0 $ y tip_amount < = 5 $<br /><br />Clase 2: tip_amount > 5 $ y tip_amount < = 10 $<br /><br />Clase 3: tip_amount > 10 $ y tip_amount < = 20 $<br /><br />Clase 4: tip_amount > 20 $|

## <a name="create-plots-using-r-in-t-sql"></a>Crear gráficos de uso de R en T-SQL

Dado que la visualización es una herramienta muy eficaz para comprender la distribución de los datos y los valores atípicos, R proporciona muchos paquetes para visualizar los datos. La distribución estándar de código abierto de R también incluye muchas funciones para crear histogramas, gráficos de dispersión, diagramas de caja y otros gráficos de exploración de datos.

Normalmente, R crea imágenes mediante un dispositivo de R para salida gráfica. Puede capturar la salida de este dispositivo y almacenar la imagen en un tipo de datos **varbinary** para representarla en la aplicación, o puede guardar las imágenes en cualquiera de los formatos de archivo compatibles (.JPG, .PDF, etc.).

En esta sección, aprenderá a trabajar con cada tipo de salida mediante procedimientos almacenados. El proceso general es como sigue:

- Crear un procedimiento almacenado para generar un gráfico de R como datos varbinary

- Generar el trazado y guardarlo en un archivo de imagen

- Utilizar un procedimiento almacenado para convertir los datos binarios de trazado en un archivo JPG o PDF

### <a name="create-the-stored-procedure-plothistogram"></a>Crear el procedimiento almacenado PlotHistogram

1. Para crear el gráfico, use `rxHistogram`, una de las funciones de R mejoradas que se proporcionan en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]para trazar un histograma en función de los datos de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Para facilitar la llamada a la función R, la encapsulará en un procedimiento almacenado, _PlotHistogram_.

    En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una nueva **consulta** ventana.

2. En la base de datos que contiene los datos del tutoriales, cree el procedimiento con esta instrucción:

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =  
      N'SELECT tipped FROM nyctaxi_sample'  
      EXECUTE sp_execute_external_script @language = N'R',  
                                         @script = N'  
       image_file = tempfile();  
       jpeg(filename = image_file);  
       #Plot histogram  
       rxHistogram(~tipped, data=InputDataSet, col=''lightgreen'',   
       title = ''Tip Histogram'', xlab =''Tipped or not'', ylab =''Counts'');  
       dev.off();  
       OutputDataSet <- data.frame(data=readBin(file(image_file, "rb"), what=raw(), n=1e6));  
       ',  
       @input_data_1 = @query  
       WITH RESULT SETS ((plot varbinary(max)));  
    END
    GO
    ```

    Asegúrese de modificar el código para usar el nombre de tabla correcto, si es necesario.
  
    -   La variable `@query` define el texto de consulta (`'SELECT tipped FROM nyctaxi_sample'`), que se pasa al script de R como argumento para la variable de entrada de script `@input_data_1`.
  
    -   El script de R es bastante sencillo: una variable de R (`image_file`) se define para almacenar la imagen y, después, se llama a la función `rxHistogram` para generar el trazado.
  
    -   El dispositivo de R se establece en **desactivado**.
  
        En R, al enviar un comando de trazado de alto nivel, R abrirá una ventana de gráficos, denominada *dispositivo*. Puede cambiar el tamaño, los colores y otros aspectos de la ventana, o puede desconectar el dispositivo si está escribiendo en un archivo o controlando la salida de algún otro modo.
  
    -   El objeto de gráficos de R se serializa en un data.frame de R para la salida.

### <a name="generate-the-graphics-data-and-save-to-file"></a>Generar los datos de gráficos y guardar en archivo

El procedimiento almacenado devuelve la imagen como una secuencia de datos varbinary, que, evidentemente, no puede ver directamente. En cambio, puede usar la utilidad **bcp** para obtener los datos varbinary y guardarlos como un archivo de imagen en un equipo cliente.
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la instrucción siguiente:
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **Resultado**
    
    *plot*
    *0xFFD8FFE000104A4649...*
  
2.  Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando, y proporcione el nombre de instancia adecuado, el nombre de la base de datos, el nombre de usuario y las credenciales como argumentos:
  
     ```
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Modificadores de comandos bcp distinguen mayúsculas de minúsculas.
  
3.  Si la conexión es correcta, se le pedirá que escriba más información sobre el formato de archivo de gráficos. Pulse ENTRAR en cada aviso para aceptar los valores predeterminados, excepto estos cambios:
  
    -   En **prefix-length of field plot**, escriba 0
  
    -   Escriba **Y** si quiere guardar los parámetros de salida para un uso posterior.
  
    ```
    Enter the file storage type of field plot [varbinary(max)]:
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **Resultado**
    
    ```
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > Si guarda la información de formato en archivo (bcp.fmt), la utilidad **bcp** genera una definición de formato que puede aplicar a los comandos similares en el futuro sin tener que cambiar las opciones de formato de archivo de gráficos. Para usar el archivo de formato, agregue `-f bcp.fmt` al final de cualquier línea de comandos después del argumento de la contraseña.
  
4.  El archivo de salida se creará en el mismo directorio en el que se ha ejecutado el comando de PowerShell. Para ver el trazado, basta con abrir el archivo plot.jpg.
  
    ![desplazamientos en taxi con y sin propinas](media/rsql-devtut-tippedornot.jpg "desplazamientos en taxi con y sin propinas")  
  
### <a name="export-the-plot-data-to-a-viewable-file"></a>Exportar los datos de gráfico a un archivo visible

Salida de un trazado de R para datos binarios tipo puede ser conveniente para su uso por aplicaciones, pero no resulta muy útil para un científico de datos que necesita el trazado representado durante la fase de exploración de datos. Normalmente, los científicos de datos generarán varias visualizaciones de datos, para obtener información sobre los datos desde distintas perspectivas.

Para generar gráficos para que los usuarios, puede usar un procedimiento almacenado que crea la salida de R en formatos populares, como. JPG. PDF, y. PNG. Después de que el procedimiento almacenado cree el gráfico, solo tiene que abrir el archivo para visualizar el trazado.

1. Crear un nuevo procedimiento almacenado, _PlotInOutputFiles_, que muestra cómo escribir histogramas, scatterplots y otros gráficos de R a. JPG y. Formato PDF.

    En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una nueva **consulta** ventana y péguelo en el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles]  
    AS  
    BEGIN  
      SET NOCOUNT ON;  
      DECLARE @query nvarchar(max) =  
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'  
      EXECUTE sp_execute_external_script @language = N'R',  
      @script = N'  
       # Set output directory for files and check for existing files with same names   
        mainDir <- ''C:\\temp\\plots''  
        dir.create(mainDir, recursive = TRUE, showWarnings = FALSE)  
        setwd(mainDir);  
        print("Creating output plot files:", quote=FALSE)
        
        # Open a jpeg file and output histogram of tipped variable in that file.  
        dest_filename = tempfile(pattern = ''rHistogram_Tipped_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.jpg'',sep="")  
        print(dest_filename, quote=FALSE);  
        jpeg(filename=dest_filename);  
        hist(InputDataSet$tipped, col = ''lightgreen'', xlab=''Tipped'',   
            ylab = ''Counts'', main = ''Histogram, Tipped'');  
         dev.off();  

        # Open a pdf file and output histograms of tip amount and fare amount.   
        # Outputs two plots in one row  
        dest_filename = tempfile(pattern = ''rHistograms_Tip_and_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=7);  
        par(mfrow=c(1,2));  
        hist(InputDataSet$tip_amount, col = ''lightgreen'',   
            xlab=''Tip amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram, Tip amount'', xlim = c(0,40), 100);  
        hist(InputDataSet$fare_amount, col = ''lightgreen'',   
            xlab=''Fare amount ($)'',   
            ylab = ''Counts'',   
            main = ''Histogram,   
            Fare amount'',   
            xlim = c(0,100), 100);  
       dev.off();  
  
        # Open a pdf file and output an xyplot of tip amount vs. fare amount using lattice;  
        # Only 10,000 sampled observations are plotted here, otherwise file is large.  
        dest_filename = tempfile(pattern = ''rXYPlots_Tip_vs_Fare_Amount_'', tmpdir = mainDir)  
        dest_filename = paste(dest_filename, ''.pdf'',sep="")  
        print(dest_filename, quote=FALSE);  
        pdf(file=dest_filename, height=4, width=4);  
        plot(tip_amount ~ fare_amount,   
            data = InputDataSet[sample(nrow(InputDataSet), 10000), ],   
            ylim = c(0,50),   
            xlim = c(0,150),   
            cex=.5,   
            pch=19,   
            col=''darkgreen'',    
            main = ''Tip amount by Fare amount'',   
            xlab=''Fare Amount ($)'',   
            ylab = ''Tip Amount ($)'');   
        dev.off();',  
     @input_data_1 = @query  
     END
    ```
  
    -   El resultado de la consulta SELECT en el procedimiento almacenado se almacena en la trama de datos predeterminada de R, `InputDataSet`. Se puede llamar a varias funciones de trazado de R para generar los archivos de gráficos reales.
  
        La mayoría de los scripts insertados de R representan las opciones de estas funciones de gráficos, como `plot` o `hist`.
  
    -   Todos los archivos se guardan en la carpeta local _C:\temp\Plots\\_. La carpeta de destino se define mediante los argumentos proporcionados para el script de R como parte del procedimiento almacenado.  Para cambiar la carpeta de destino, cambie el valor de la variable `mainDir`.
  
2.  Ejecute la instrucción para crear el procedimiento almacenado.

    ```SQL
    EXEC PlotInOutputFiles
    ```

    **Resultado**
    
    ```
    STDOUT message(s) from external script:
    [1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 
    
    C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]
    
    C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
    ```

    Los números de los nombres de archivo se generan de forma aleatoria para asegurarse de que no obtendrá un error al intentar escribir en un archivo existente.

3. Para ver el trazado, abra la carpeta de destino y revise los archivos creados por el código de R en el procedimiento almacenado.

    + El archivo `rHistogram_Tipped.jpg` muestra el número de viajes que se obtuvo una sugerencia frente a los viajes que se obtuvo ninguna sugerencia. (Este histograma es igual que generó en el paso anterior).

    + El archivo `rHistograms_Tip_and_Fare_Amount.pdf` muestra la distribución de los importes de sugerencia, trazadas en las cantidades de tarifa.
    
    ![histograma que muestra tip_amount y fare_amount](media/rsql-devtut-tipamtfareamt.PNG "histograma que muestra tip_amount y fare_amount")

    + El archivo `rXYPlots_Tip_vs_Fare_Amount.pdf` contiene un scatterplot con la cantidad de tarifa en el eje x y la cantidad de sugerencia en el eje y.

    ![cantidad de sugerencia traza por encima de cantidad de tarifa](media/rsql-devtut-tipamtbyfareamt.PNG "cantidad de sugerencia traza por encima de cantidad de tarifa")

2.  Para generar los archivos en una carpeta diferente, cambie el valor de la variable `mainDir` en el script insertado de R en el procedimiento almacenado. También puede modificar el script para generar diferentes formatos, más archivos, etc.

## <a name="next-lesson"></a>Lección siguiente

[Lección 4: Crear características de datos mediante T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 2: Importar datos a SQL Server usando PowerShell](../r/sqldev-import-data-to-sql-server-using-powershell.md)
