---
title: Lección 1 explorar y visualizar datos mediante R y T-SQL
description: Tutorial que muestra cómo explorar y visualizar datos de SQL Server con funciones de R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/29/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2c204e06edd830d8036b6d0119ce1aff1a9c6833
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715370"
---
# <a name="lesson-1-explore-and-visualize-the-data"></a>Lección 1: Explore y visualice los datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En este paso, revisará los datos de ejemplo y, a continuación, generará algunos trazados mediante [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) de [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) y la función de [hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) genérica en base R. Estas funciones de R ya están incluidas [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]en.

Un objetivo clave de esta lección es mostrar cómo llamar a las funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] R desde en procedimientos almacenados y guardar los resultados en formatos de archivo de aplicación:

+ Cree un procedimiento almacenado mediante **RxHistogram** para generar un trazado de R como datos varbinary. Use **BCP** para exportar el flujo binario a un archivo de imagen.
+ Cree un procedimiento almacenado mediante **hist** para generar un trazado y guardar los resultados como salida jpg y PDF.

> [!NOTE]
> Dado que la visualización es una herramienta muy eficaz para comprender la forma de datos y la distribución, R proporciona una variedad de funciones y paquetes para generar histogramas, gráficos de dispersión, gráficos de cuadros y otros gráficos de exploración de datos. R normalmente crea imágenes mediante un dispositivo de R para la salida gráfica, que se puede capturar y almacenar como un tipo de datos **varbinary** para su representación en la aplicación. También puede guardar las imágenes en cualquiera de los formatos de archivo de soporte (. JPG,. PDF, etc.).

## <a name="review-the-data"></a>Revisar los datos

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Primero Tómese un minuto para revisar los datos de ejemplo, si no lo ha hecho ya.

En el conjunto de documentos público original, los identificadores de taxi y los registros de viaje se proporcionaron en archivos independientes. Sin embargo, para facilitar el uso de los datos de ejemplo, los dos conjuntos de datos originales se han unido en las columnas _Medallion_, _hack\_License_y _pickup\_DateTime_.  Los registros también se muestrearon para obtener solo un 1 % del número de registros original. El conjunto de datos muestreado resultante tiene 1 703 957 filas y 23 columnas.

**Identificadores de taxis**
  
-   La columna _Medallion_ representa el número de identificación único del taxi.
  
-   La _columna\_Hacke License_ contiene el número de licencia del controlador de taxi (anónimos).
  
**Registros de viajes y tarifas**
  
-   Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.
  
-   Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.
  
-   Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático. La _columna\_Tip amount_ contiene valores numéricos continuos y se puede usar como columna de **etiqueta** para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. La columna de _clase\_Tip_ tiene varias **etiquetas de clase** y, por tanto, se puede usar como etiqueta para las tareas de clasificación de varias clases.
  
    Este tutorial muestra solo la tarea de clasificación binaria; puede intentar crear modelos de las otras dos tareas de aprendizaje automático, regresión y clasificación de varias clases.
  
-   Los valores que se usan para las columnas de etiqueta se basan en la columna _Tip\_amount_ , con las siguientes reglas de negocios:
  
    |Nombre de columna derivada|Regla|
    |-|-|
     |tipped|Si tip_amount > 0, tipped = 1, de lo contrario, tipped = 0|
    |tip_class|Clase 0: tip_amount = 0 $<br /><br />Clase 1: tip_amount > 0 $ y tip_amount < = 5 $<br /><br />Clase 2: tip_amount > 5 $ y tip_amount < = 10 $<br /><br />Clase 3: tip_amount > 10 $ y tip_amount < = 20 $<br /><br />Clase 4: tip_amount > 20 $|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>Crear un procedimiento almacenado mediante rxHistogram para trazar los datos

Para crear el trazado, use [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), una de las funciones mejoradas de R proporcionadas en [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). Este paso traza un histograma en función de los datos de [!INCLUDE[tsql](../../includes/tsql-md.md)] una consulta. Puede encapsular esta función en un procedimiento almacenado, **PlotRxHistogram**.

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en explorador de objetos, haga clic con el botón secundario en la base de datos **NYCTaxi_Sample** y seleccione **nueva consulta**.

2. Pegue el siguiente script para crear un procedimiento almacenado que represente el histograma. Este ejemplo se denomina **RPlotRxHistogram*.

    ```sql
    CREATE PROCEDURE [dbo].[RxPlotHistogram]
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

Entre los puntos clave que se deben comprender en este script se incluyen los siguientes: 
  
+ La variable `@query` define el texto de consulta (`'SELECT tipped FROM nyctaxi_sample'`), que se pasa al script de R como argumento para la variable de entrada de script `@input_data_1`. En el caso de los scripts de R que se ejecutan como procesos externos, debe tener una asignación uno a uno entre las entradas del script y las entradas al procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) que inicia la sesión de R en SQL Server.
  
+ Dentro del script de R, se define`image_file`una variable () para almacenar la imagen. 

+ Se llama a la función **rxHistogram** de la biblioteca RevoScaleR para generar el trazado.
  
+ El dispositivo R está establecido en **OFF** porque está ejecutando este comando como un script externo en SQL Server. Normalmente en R, cuando se emite un comando de trazado de nivel alto, R abre una ventana de gráficos, denominada *dispositivo*. Puede desactivar el dispositivo si está escribiendo en un archivo o controlando el resultado de otra manera.
  
+ El objeto de gráficos de R se serializa en un data.frame de R para la salida.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>Ejecutar el procedimiento almacenado y usar BCP para exportar datos binarios a un archivo de imagen

El procedimiento almacenado devuelve la imagen como una secuencia de datos varbinary, que, evidentemente, no puede ver directamente. En cambio, puede usar la utilidad **bcp** para obtener los datos varbinary y guardarlos como un archivo de imagen en un equipo cliente.
  
1. En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la instrucción siguiente:
  
    ```sql
    EXEC [dbo].[RxPlotHistogram]
    ```
  
    **Resultado**
    
    *trazado* *0xFFD8FFE000104A4649...*
  
2. Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando, proporcionando el nombre de la instancia, el nombre de la base de datos, el nombre de usuario y las credenciales correspondientes como argumentos. En el caso de los usuarios que usan identidades de Windows, puede reemplazar **-U** y **-P** por **-T**.
  
    ```powershell
    bcp "exec RxPlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  NYCTaxi_Sample  -U <user name> -P <password> -T
    ```

    > [!NOTE]
    > Los modificadores de comandos para BCP distinguen mayúsculas de minúsculas.
  
3. Si la conexión es correcta, se le pedirá que escriba más información sobre el formato de archivo de gráficos. 

   Pulse ENTRAR en cada aviso para aceptar los valores predeterminados, excepto estos cambios:
    
   + En **prefix-length of field plot**, escriba 0
  
   + Escriba **Y** si quiere guardar los parámetros de salida para un uso posterior.
  
    ```powershell
    Enter the file storage type of field plot [varbinary(max)]: 
    Enter prefix-length of field plot [8]: 0
    Enter length of field plot [0]:
    Enter field terminator [none]:
  
    Do you want to save this format information in a file? [Y/n]
    Host filename [bcp.fmt]:
    ```
  
    **Resultado**
    
    ```powershell
    Starting copy...
    1 rows copied.
    Network packet size (bytes): 4096
    Clock Time (ms.) Total     : 3922   Average : (0.25 rows per sec.)
    ```

    > [!TIP]
    > Si guarda la información de formato en archivo (bcp.fmt), la utilidad **bcp** genera una definición de formato que puede aplicar a los comandos similares en el futuro sin tener que cambiar las opciones de formato de archivo de gráficos. Para usar el archivo de formato, agregue `-f bcp.fmt` al final de cualquier línea de comandos después del argumento de la contraseña.
  
4.  El archivo de salida se creará en el mismo directorio en el que se ha ejecutado el comando de PowerShell. Para ver el trazado, basta con abrir el archivo plot.jpg.
  
    ![desplazamientos en taxi con y sin propinas](media/rsql-devtut-tippedornot.jpg "desplazamientos en taxi con y sin propinas")  
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Crear un procedimiento almacenado mediante hist y varios formatos de salida

Normalmente, los científicos de datos generan varias visualizaciones de datos para obtener información sobre los datos de diferentes perspectivas. En este ejemplo, creará un procedimiento almacenado denominado **RPlotHist** para escribir histogramas, gráficos y otros gráficos de R en. JPG y. Formato PDF.

Este procedimiento almacenado utiliza la función de **hist** para crear el histograma, exportando los datos binarios a formatos populares como. JPG,. PDF y. Dicho. 

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en explorador de objetos, haga clic con el botón secundario en la base de datos **NYCTaxi_Sample** y seleccione **nueva consulta**.

2. Pegue el siguiente script para crear un procedimiento almacenado que represente el histograma. Este ejemplo se denomina **RPlotHist** .
  
    ```sql
    CREATE PROCEDURE [dbo].[RPlotHist]  
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
  
+ El resultado de la consulta SELECT en el procedimiento almacenado se almacena en la trama de datos predeterminada de R, `InputDataSet`. Se puede llamar a varias funciones de trazado de R para generar los archivos de gráficos reales. La mayoría de los scripts insertados de R representan las opciones de estas funciones de gráficos, como `plot` o `hist`.
  
+ Todos los archivos se guardan en la carpeta local C:\temp\Plots. La carpeta de destino se define mediante los argumentos proporcionados para el script de R como parte del procedimiento almacenado.  Para cambiar la carpeta de destino, cambie el valor de la variable `mainDir`.

+ Para generar los archivos en una carpeta diferente, cambie el valor de la variable `mainDir` en el script insertado de R en el procedimiento almacenado. También puede modificar el script para generar diferentes formatos, más archivos, etc.

### <a name="execute-the-stored-procedure"></a>Ejecutar el procedimiento almacenado

Ejecute la siguiente instrucción para exportar datos de trazados binarios a formatos de archivo JPEG y PDF.

```sql
EXEC RPlotHist
```

**Resultado**
    
```sql
STDOUT message(s) from external script:
[1] Creating output plot files:[1] C:\temp\plots\rHistogram_Tipped_18887f6265d4.jpg[1] 

C:\temp\plots\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]

C:\temp\plots\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf
```

Los números de los nombres de archivo se generan de forma aleatoria para asegurarse de que no recibe un error al intentar escribir en un archivo existente.

### <a name="view-output"></a>Ver resultados 

Para ver el trazado, abra la carpeta de destino y revise los archivos creados por el código R en el procedimiento almacenado.

1. Vaya a la carpeta indicada en el mensaje STDOUT (en el ejemplo, es C:\temp\plots\)

2. Abra `rHistogram_Tipped.jpg` para mostrar el número de viajes que obtuvieron una propina frente a los viajes que no se han encontrado. (Este histograma es muy similar al que se generó en el paso anterior).

3. Abra `rHistograms_Tip_and_Fare_Amount.pdf` para ver la distribución de los importes de las propinas, trazadas con respecto a las cantidades de tarifas.
    
  ![histograma que muestra tip_amount y fare_amount](media/rsql-devtut-tipamtfareamt.PNG "histograma que muestra tip_amount y fare_amount")

4. Abra `rXYPlots_Tip_vs_Fare_Amount.pdf` para ver un dispersión con el importe de la tarifa en el eje x y el importe de la propina en el eje y.

   ![importe de propina trazado por importe de tarifa](media/rsql-devtut-tipamtbyfareamt.PNG "importe de propina trazado por importe de tarifa")

## <a name="next-lesson"></a>Lección siguiente

[Lección 2: Crear características de datos mediante T-SQL](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lección anterior

[Configuración de datos de demostración de taxis de Nueva York](demo-data-nyctaxi-in-sql.md)
