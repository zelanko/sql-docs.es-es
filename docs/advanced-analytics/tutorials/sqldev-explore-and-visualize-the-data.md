---
title: Lección 3 explorar y visualizar datos mediante R y T-SQL (SQL Server Machine Learning) | Microsoft Docs
description: Tutorial que muestra cómo insertar código de R en SQL Server los procedimientos almacenados y funciones de Transact-SQL
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6b34de3c71629a1563bf0d480306680dc6253748
ms.sourcegitcommit: 320958d0f55b6974abf46f8a04f7a020ff86a0ae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703628"
---
# <a name="lesson-3-explore-and-visualize-the-data"></a>Lección 3: Explorar y visualizar los datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo forma parte de un tutorial para desarrolladores de SQL sobre cómo usar R en SQL Server.

En esta lección, podrá revisar los datos de ejemplo y, a continuación, generará algunos trazados mediante [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) desde [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) y genérico [Hist](https://www.rdocumentation.org/packages/graphics/versions/3.5.0/topics/hist) función en r de base. Estas funciones de R ya están incluidas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Un objetivo clave es que muestra cómo llamar a funciones de R desde [!INCLUDE[tsql](../../includes/tsql-md.md)] en procedimientos almacenados y guardar los resultados en formatos de archivo de aplicación:

+ Crear un procedimiento almacenado mediante **RxHistogram** para generar un trazado de R como datos varbinary. Use **bcp** para exportar la secuencia binaria a un archivo de imagen.
+ Crear un procedimiento almacenado mediante **Hist** para generar un trazado, guardar los resultados como salida JPG y PDF.

> [!NOTE]
> Porque la visualización es una herramienta eficaz para comprender la forma de datos y la distribución, R proporciona una gama de funciones y paquetes para generar los histogramas, gráficos de dispersión, caja y otros gráficos de exploración de datos. Normalmente, R crea imágenes mediante un dispositivo de R para salida gráfica, lo que puede capturar y almacenar como un **varbinary** tipo de datos para la representación en la aplicación. También puede guardar las imágenes a cualquiera de los formatos de archivo de soporte técnico (. JPG. PDF, etcetera).

## <a name="review-the-data"></a>Revise los datos

Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. Primero, tómese un minuto para revisar los datos de ejemplo, si no lo ha hecho ya.

En el conjunto de datos original, los identificadores de taxis y los registros de viaje se proporcionaron en archivos independientes. Sin embargo, para que los datos de ejemplo más fácil de usar, los dos conjuntos de datos originales se han unido en las columnas _medallion_, _hack\_licencia_, y _pickup\_ fecha y hora_.  Los registros también se muestrearon para obtener solo un 1 % del número de registros original. El conjunto de datos muestreado resultante tiene 1 703 957 filas y 23 columnas.

**Identificadores de taxis**
  
-   La columna _medallion_ representa el número de identificador único del taxi.
  
-   El _hack\_licencia_ columna contiene el número de licencia del conductor del taxi (anónimo).
  
**Registros de viajes y tarifas**
  
-   Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.
  
-   Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.
  
-   Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático. El _sugerencia\_cantidad_ columna contiene valores numéricos continuos y se puede usar como el **etiqueta** columna para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. El _sugerencia\_clase_ columna tiene varios **etiquetas de clase** y, por tanto, se puede usar como etiqueta para tareas de clasificación multiclase.
  
    Este tutorial muestra solo la tarea de clasificación binaria; puede intentar crear modelos de las otras dos tareas de aprendizaje automático, regresión y clasificación de varias clases.
  
-   Los valores utilizados para las columnas de etiqueta se basan en el _sugerencia\_cantidad_ columna, utilizando estas reglas de negocios:
  
    |Nombre de columna derivada|Regla|
    |-|-|
     |tipped|Si tip_amount > 0, tipped = 1, de lo contrario, tipped = 0|
    |tip_class|Clase 0: tip_amount = 0 $<br /><br />Clase 1: tip_amount > 0 $ y tip_amount < = 5 $<br /><br />Clase 2: tip_amount > 5 $ y tip_amount < = 10 $<br /><br />Clase 3: tip_amount > 10 $ y tip_amount < = 20 $<br /><br />Clase 4: tip_amount > 20 $|

## <a name="create-a-stored-procedure-using-rxhistogram-to-plot-the-data"></a>Crear un procedimiento almacenado, el uso de rxHistogram para trazar los datos

Para crear el trazado, use [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram), una de las funciones mejoradas de R proporcionadas en [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). Este paso traza un histograma según datos de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Puede ajustar esta función en un procedimiento almacenado, **PlotHistogram**.

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, haga clic en el **NYCTaxi_Sample** de base de datos, expanda **programación**y, a continuación, expanda **Stored Procedures** para ver el procedimientos creados en la lección 2.

2. Haga clic en **PlotHistogram** y seleccione **modificar** para ver el código fuente. Puede ejecutar este procedimiento para llamar a **rxHistogram** sobre los datos contenidos en la columna de tabla nyctaxi_sample superpuesta.

3. Si lo desea, como un ejercicio de aprendizaje, cree su propia copia de este procedimiento almacenado mediante el ejemplo siguiente. Abra una nueva ventana de consulta y pegue en el siguiente script para crear un procedimiento almacenado que traza el histograma. En este ejemplo se denomina **PlotHistogram2** para evitar colisiones de nomenclatura con el procedimiento existente.

    ```SQL
    CREATE PROCEDURE [dbo].[PlotHistogram2]
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

El procedimiento almacenado **PlotHistogram2** es idéntico a un procedimiento almacenado preexistente **PlotHistogram** creado por el `RunSQL_SQL_Walkthrough.ps1` secuencia de comandos. 
  
+ La variable `@query` define el texto de consulta (`'SELECT tipped FROM nyctaxi_sample'`), que se pasa al script de R como argumento para la variable de entrada de script `@input_data_1`.
  
+ El script de R es bastante sencillo: una variable de R (`image_file`) se define para almacenar la imagen y, a continuación, el **rxHistogram** función se invoca para generar el trazado.
  
+ El dispositivo de R se establece en **desactivar** porque se está ejecutando este comando como un script externo en SQL Server. Normalmente en R, al emitir un comando de trazado de alto nivel, R abrirá una ventana de gráficos que llama a un *dispositivo*. Puede cambiar el tamaño, los colores y otros aspectos de la ventana, o puede desconectar el dispositivo si está escribiendo en un archivo o controlando la salida de algún otro modo.
  
+ El objeto de gráficos de R se serializa en un data.frame de R para la salida.

### <a name="execute-the-stored-procedure-and-use-bcp-to-export-binary-data-to-an-image-file"></a>Ejecute el procedimiento almacenado y el uso de bcp para exportar los datos binarios a un archivo de imagen

El procedimiento almacenado devuelve la imagen como una secuencia de datos varbinary, que, evidentemente, no puede ver directamente. En cambio, puede usar la utilidad **bcp** para obtener los datos varbinary y guardarlos como un archivo de imagen en un equipo cliente.
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la instrucción siguiente:
  
    ```SQL
    EXEC [dbo].[PlotHistogram]
    ```
  
    **Resultado**
    
    *plot*
    *0xFFD8FFE000104A4649...*
  
2.  Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando, que proporciona el nombre de instancia adecuado, el nombre de base de datos, nombre de usuario y las credenciales como argumentos. Para aquellos que usen las identidades de Windows, puede reemplazar **- U** y **-P** con **-T**.
  
     ```text
     bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  TaxiNYC_Sample  -U <user name> -P <password>
     ```

    > [!NOTE]
    > Modificadores de comandos bcp distinguen mayúsculas de minúsculas.
  
3.  Si la conexión es correcta, se le pedirá que escriba más información sobre el formato de archivo de gráficos. 

   Pulse ENTRAR en cada aviso para aceptar los valores predeterminados, excepto estos cambios:
    
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
  
## <a name="create-a-stored-procedure-using-hist-and-multiple-output-formats"></a>Crear un procedimiento almacenado mediante Hist y varios formatos de salida

Normalmente, los científicos de datos generan varias visualizaciones de datos para obtener información sobre los datos desde distintas perspectivas. En este ejemplo, el procedimiento almacenado usa la función Hist para crear el histograma, exportar los datos binarios a formatos populares como. JPG. PDF, y. PNG. 

1. Use el procedimiento almacenado existente, **PlotInOutputFiles**, escribir histogramas, gráficos de dispersión y otros gráficos de R a. JPG y. Formato PDF. El `RunSQL_SQL_Walkthrough.ps1` crea **PlotInOutputFiles** y se agrega la base de datos. Utilice el botón secundario **modificar** para ver el código fuente.

2. Opcionalmente, como un ejercicio de aprendizaje, cree su propia copia del procedimiento como **PlotInOutputFiles2**, con un nombre único para evitar un conflicto de nomenclatura.

    En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una nueva **consulta** ventana y péguelo en el siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.
  
    ```SQL
    CREATE PROCEDURE [dbo].[PlotInOutputFiles2]  
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
  
+ Todos los archivos se guardan en la carpeta local _C:\temp\Plots\\_. La carpeta de destino se define mediante los argumentos proporcionados para el script de R como parte del procedimiento almacenado.  Para cambiar la carpeta de destino, cambie el valor de la variable `mainDir`.

+ Para generar los archivos en una carpeta diferente, cambie el valor de la variable `mainDir` en el script insertado de R en el procedimiento almacenado. También puede modificar el script para generar diferentes formatos, más archivos, etc.

### <a name="execute-the-stored-procedure"></a>Ejecutar el procedimiento almacenado

Ejecute la instrucción siguiente para exportar datos de trazado binario a formatos de archivo JPEG y PDF.

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

Los números de los nombres de archivo se generan aleatoriamente para garantizar que no tienen un error al intentar escribir en un archivo existente.

### <a name="view-output"></a>Ver la salida 

Para ver el trazado, abra la carpeta de destino y revise los archivos creados por el código de R en el procedimiento almacenado.

1. Vaya a la carpeta indicada en el mensaje STDOUT (en el ejemplo, esto es C:\temp\plots\)

2. Abra `rHistogram_Tipped.jpg` para mostrar el número de viajes en los que se ha recibido una propina frente a los viajes que se ha recibido ninguna propina. (Este histograma es parecido al que ha generado en el paso anterior).

3. Abra `rHistograms_Tip_and_Fare_Amount.pdf` para ver la distribución de propinas trazado en las cantidades de tarifas.
    
  ![histograma que muestra tip_amount y fare_amount](media/rsql-devtut-tipamtfareamt.PNG "histograma que muestra tip_amount y fare_amount")

4. Abra `rXYPlots_Tip_vs_Fare_Amount.pdf` para ver un gráfico de dispersión con el importe en el eje x y la cantidad de propina en el eje y.

   ![propina traza a través de importe de](media/rsql-devtut-tipamtbyfareamt.PNG "propina traza a través de importe de la")

## <a name="next-lesson"></a>Lección siguiente

[Lección 3: Crear características de datos mediante T-SQL](sqldev-create-data-features-using-t-sql.md)

## <a name="previous-lesson"></a>Lección anterior

[Lección 1: Configurar los datos de demostración de taxis de Nueva York](sqldev-download-the-sample-data.md)
