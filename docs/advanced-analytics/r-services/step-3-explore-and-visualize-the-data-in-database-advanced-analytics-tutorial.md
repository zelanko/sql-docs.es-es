---
title: "Paso 3: Explorar y visualizar los datos (Tutorial de an&#225;lisis avanzado en base de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 7fe670f3-5e62-43ef-97eb-b9af54df9128
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Paso 3: Explorar y visualizar los datos (Tutorial de an&#225;lisis avanzado en base de datos)
Desarrollar una solución de ciencia de datos incluye normalmente la exploración de datos intensivos y la visualización de datos. En este paso, revisará los datos de ejemplo y, después, generará algunos trazados mediante las funciones de R. Estas funciones de R ya están incluidas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]; en este tutorial, practicará la llamada a funciones de R desde [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## Revisar los datos  
En primer lugar, revise los datos de ejemplo si no lo ha hecho ya, solo le llevará un minuto.  
  
En el conjunto de datos original, los identificadores de taxis y los registros de viaje se proporcionaron en archivos independientes. En cambio, para facilitar el uso de los datos de ejemplo, los dos conjuntos de datos originales se han unido en las columnas _medallion_, _hack_license_ y _pickup_datetime_.  Los registros también se muestrearon para obtener solo un 1 % del número de registros original. El conjunto de datos muestreado resultante tiene 1 703 957 filas y 23 columnas.  
  
**Identificadores de taxis**  
  
-   La columna _medallion_ representa el número de identificador único del taxi.  
  
-   La columna _hack_license_ contiene el número de licencia del conductor del taxi (anónimo).  
  
**Registros de viajes y tarifas**  
  
-   Cada registro de viaje incluye la ubicación y hora de recogida y destino y la distancia del viaje.  
  
-   Cada registro de tarifa incluye información de pago, como el tipo de pago, el importe total de pago y la cantidad de propina.  
  
-   Las últimas tres columnas se pueden usar para varias tareas de aprendizaje automático.  La columna _tip_amount_ contiene valores numéricos continuos y se puede usar como la columna **label** para el análisis de regresión. La columna _tipped_ tiene solo valores sí/no y se usa para la clasificación binaria. La columna _tip_class_ tiene varias **etiquetas de clase** y, por tanto, se puede usar como etiqueta para tareas de clasificación de varias clases.  
  
    Este tutorial muestra solo la tarea de clasificación binaria; puede intentar crear modelos de las otras dos tareas de aprendizaje automático, regresión y clasificación de varias clases.  
  
-   Los valores usados para las columnas de etiqueta se basan en la columna _tip_amount_, usando estas reglas de negocios:  
  
    |Nombre de columna derivada|Regla|  
    |-|-|  
     |tipped|Si tip_amount > 0, tipped = 1, de lo contrario, tipped = 0|  
    |tip_class|Clase 0: tip_amount = 0 $<br /><br />Clase 1: tip_amount > 0 $ y tip_amount < = 5 $<br /><br />Clase 2: tip_amount > 5 $ y tip_amount < = 10 $<br /><br />Clase 3: tip_amount > 10 $ y tip_amount < = 20 $<br /><br />Clase 4: tip_amount > 20 $|  
  
## Crear trazados con R en T-SQL  
Dado que la visualización es una herramienta muy eficaz para comprender la distribución de los datos y los valores atípicos, R proporciona muchos paquetes para visualizar los datos. La distribución estándar de código abierto de R también incluye muchas funciones para crear histogramas, gráficos de dispersión, diagramas de caja y otros gráficos de exploración de datos.  
  
Normalmente, R crea imágenes mediante un dispositivo de R para salida gráfica. Puede capturar la salida de este dispositivo y almacenar la imagen en un tipo de datos **varbinary** para representarla en la aplicación, o puede guardar las imágenes en cualquiera de los formatos de archivo compatibles (.JPG, .PDF, etc.).  
  
En esta sección, aprenderá a trabajar con cada tipo de salida mediante procedimientos almacenados.  
  
-   Almacenar trazados como tipo de datos varbinary  
  
-   Guardar trazados en archivos (.JPG, .PDF) en el servidor  
  
### Almacenar trazados como tipo de datos varbinary  
Usará `rxHistogram`, una de las funciones mejoradas de R proporcionadas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para trazar un histograma según datos de una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para facilitar la llamada a la función R, la encapsulará en un procedimiento almacenado, _PlotHistogram_.  
  
El procedimiento almacenado devuelve la imagen como una secuencia de datos varbinary, que, evidentemente, no puede ver directamente. En cambio, puede usar la utilidad **bcp** para obtener los datos varbinary y guardarlos como un archivo de imagen en un equipo cliente.  
  
##### Para crear el procedimiento almacenado PlotHistogram  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una nueva ventana de consulta.  
  
2.  Seleccione la base de datos para el tutorial y cree el procedimiento con esta instrucción.  
  
    ```  
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
  
    -   El objeto de gráficos de R se serializa en un data.frame de R para la salida. Se trata de una solución temporal para CTP3.  
  
##### Para mostrar datos varbinary en archivo de gráficos visibles  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la instrucción siguiente:  
  
    ```  
    EXEC [dbo].[PlotHistogram]  
    ```  
  
**Resultado**  
  
*trazado*  
*0xFFD8FFE000104A4649...*  
  
2.  Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando, y proporcione el nombre de instancia adecuado, el nombre de la base de datos, el nombre de usuario y las credenciales como argumentos:  
  
    ```  
    bcp "exec PlotHistogram" queryout "plot.jpg" -S <SQL Server instance name> -d  <database name>  -U <user name> -P <password>  
  
    ```  
  
    > [!NOTE]  
    > Los modificadores de comandos **bcp** distinguen mayúsculas de minúsculas.  
  
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
  
*Iniciando copia...*  
*1 fila copiada.*  
*Tamaño del paquete de red (bytes): 4096*  
*Tiempo de reloj (ms.) Total: 3922 Media: (0.25 filas por s)*  
   
> [!TIP]  
 > Si guarda la información de formato en archivo (bcp.fmt), la utilidad **bcp** genera una definición de formato que puede aplicar a los comandos similares en el futuro sin tener que cambiar las opciones de formato de archivo de gráficos. Para usar el archivo de formato, agregue `-f bcp.fmt` al final de cualquier línea de comandos después del argumento de la contraseña.  
  
4.  El archivo de salida se creará en el mismo directorio en el que se ha ejecutado el comando de PowerShell. Para ver el trazado, basta con abrir el archivo plot.jpg.  
  
    ![taxi trips with and without tips](../../advanced-analytics/r-services/media/rsql-devtut-tippedornot.jpg "taxi trips with and without tips")  
  
### Guardar trazados en archivos (jpg, pdf) en el servidor  
Generar un trazado de R en un tipo de datos binarios podría ser conveniente para su consumo por las aplicaciones, pero no es muy útil para un científico de datos que necesita el trazado representado durante la fase de exploración de datos. Normalmente, los científicos de datos generarán varias visualizaciones de datos, para obtener información sobre los datos desde distintas perspectivas.  
  
Para generar gráficos que se puedan ver con mayor facilidad, puede usar un procedimiento almacenado que cree la salida de R en formatos populares como .JPG, .PDF y .PNG. Después de que el procedimiento almacenado cree el gráfico, solo tiene que abrir el archivo para visualizar el trazado.  
  
En este paso, creará un nuevo procedimiento almacenado, _PlotInOutputFiles_, que muestra cómo usar las funciones de trazado de R para crear histogramas, gráficos de dispersión y mucho más en formato .JPG y .PDF. Los archivos de gráficos se guardan en archivos locales; es decir, en una carpeta en la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##### Para crear el procedimiento almacenado PlotInOutputFiles  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una ventana de consulta nueva y pegue la siguiente instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
    ```  
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
  
    -   Todos los archivos se guardan en la carpeta local _C:\temp\Plots\\_.  
  
        La carpeta de destino se define mediante los argumentos proporcionados para el script de R como parte del procedimiento almacenado.  Para cambiar la carpeta de destino, cambie el valor de la variable `mainDir`.  
  
2.  Ejecute la instrucción para crear el procedimiento almacenado.  
  
  
##### Para generar los archivos de gráficos  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute la siguiente consulta de SQL:  
  
    ```  
    EXEC PlotInOutputFiles  
  
    ```  
  
**Resultado**  
  
*Mensaje(s) STDOUT del script externo:*  
*[1] Creando archivos de trazado de salida:[1]* *C:\\\temp\\\plots\\\rHistogram_Tipped_18887f6265d4.jpg[1]* *C:\\\temp\\\plots\\\rHistograms_Tip_and_Fare_Amount_1888441e542c.pdf[1]* *C:\\\temp\\\plots\\\rXYPlots_Tip_vs_Fare_Amount_18887c9d517b.pdf*  
  
2.  Abra la carpeta de destino y revise los archivos creados por el código R en el procedimiento almacenado. (Los números de los nombres de archivo se generan de forma aleatoria).  
  
*  rHistogram_Tipped_*nnnn*.jpg: muestra el número de viajes en los que se ha recibido una propina (1) frente a los viajes en los que no se ha recibido ninguna propina (0). Este histograma es parecido al que ha generado en el paso anterior.  
  
*  rHistograms_Tip_and_Fare_Amount_*nnnn*.pdf: muestra la distribución de valores en las columnas tip_amount y fare_amount.  
  
        ![histogram showing tip_amount and fare_amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtfareamt.PNG "histogram showing tip_amount and fare_amount")  
  
*  rXYPlots_Tip_vs_Fare_Amount_*nnnn*.pdf: un gráfico de dispersión con el importe de la tarifa en el eje x y la cantidad de propina en el eje y.  
  
        ![tip amount plotted over fare amount](../../advanced-analytics/r-services/media/rsql-devtut-tipamtbyfareamt.PNG "tip amount plotted over fare amount")  
  
3.  Para generar los archivos en una carpeta diferente, cambie el valor de la variable `mainDir` en el script insertado de R en el procedimiento almacenado.  
  
    También puede modificar el script para generar diferentes formatos, más archivos, etc.  
  
## Paso siguiente  
[Paso 4: Crear características de datos mediante T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## Paso anterior  
[Paso 2: Importar datos a SQL Server mediante PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md)  
  
## Vea también  
[In-Database Advanced Analytics for SQL Developers &#40;Tutorial&#41; (Análisis avanzado en base de datos para desarrolladores de SQL &#40;Tutorial&#41;)](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
