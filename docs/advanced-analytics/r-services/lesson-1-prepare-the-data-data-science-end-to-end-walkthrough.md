---
title: "Lecci&#243;n 1: Preparar los datos (Tutorial integral de ciencia de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/18/2017"
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
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 29
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 25
---
# Lecci&#243;n 1: Preparar los datos (Tutorial integral de ciencia de datos)
Para prepararse para este tutorial, deberá hacer lo siguiente:

1. Descargue los datos y todos los scripts de R que se usan en el tutorial. Se proporciona un script de PowerShell para simplificar la descarga desde GitHub.   

2. Instale algunos paquetes de R adicionales, tanto en el servidor como en su estación de trabajo de R.  

3. Prepare el entorno, incluida la base de datos y los datos que se usan para modelado y puntuación.
 
    Para ello, usará un segundo script de PowerShell, RunSQL_R_Walkthrough.ps1.
    El script configura la base de datos y carga los datos en la tabla que se especifique.  También crea algunas funciones SQL y procedimientos almacenados que simplifican las tareas de ciencia de datos. 
 

## <a name="1-download-the-data-and-scripts"></a>1. Descargar los datos y los scripts  
Todo el código que necesitará para completar este tutorial se ha proporcionado en un repositorio de GitHub. Puede usar un script de PowerShell para crear una copia local de los archivos.  
  
#### <a name="to-download-all-scripts-using-powershell"></a>Para descargar todos los scripts con PowerShell  
  
1.  En el equipo cliente de ciencia de datos, abra un símbolo del sistema de Windows PowerShell como administrador.  
  
2.  Si no ha ejecutado PowerShell antes en esta instancia, o no tiene permiso para ejecutar scripts, es posible que se produzca un error. En ese caso, ejecute este comando antes de ejecutar el script, para permitir temporalmente permitir los scripts sin cambiar los valores predeterminados del sistema.  
  
    ```  
    Set-ExecutionPolicy Unrestricted -Scope Process -Force  
    ```  
  
3.  Ejecute el siguiente comando para descargar los archivos de script en un directorio local. Si no especifica un directorio diferente, de forma predeterminada, se crea la carpeta C:\tempR y todos los archivos se guardan ahí.  
  
    ```  
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"  
    $wc = New-Object System.Net.WebClient  
    $wc.DownloadFile($source, $ps1_dest)  
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'  
  
    ```  
  
    Si quiere guardar los archivos en un directorio diferente, edite los valores del parámetro *DestDir* y especifique una carpeta diferente en el equipo. Si escribe un nombre de carpeta que no existe, el script de PowerShell creará la carpeta automáticamente.  
  
4.  Una vez finalizada la descarga, la consola de comandos de Windows PowerShell debe ser similar a la siguiente:  
  
    ![After completion of PowerShell script](../../advanced-analytics/r-services/media/rsql-e2e-psscriptresults.PNG "After completion of PowerShell script")  
  
5.  En la consola de PowerShell, puede ejecutar el comando `ls` para ver una lista de los archivos descargados en *DestDir*.  Para ver una lista de los archivos y sus descripciones, consulte [Qué se incluye](#What-the-Download-Includes).
  
## <a name="2-install-required-packages"></a>2. Instalar los paquetes necesarios  
Este tutorial requiere algunas bibliotecas de R que no se instalan de forma predeterminada como parte de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Debe instalar los paquetes tanto en el cliente donde va a desarrollar la solución como en el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde va a implementarla.  
  
### <a name="install-required-packages-on-the-client"></a>Instalar los paquetes necesarios en el cliente  
El script de R que descargó incluye los comandos para descargar e instalar estos paquetes.  
  
1.  En su entorno de R, abra el archivo de script, RSQL_R_Walkthrough.R.  
  
2.  Resalte y ejecute estas líneas.  
  
    ```  
    # Install required R libraries for this walkthrough if they are not installed.   
  
    if (!('ggmap' %in% rownames(installed.packages()))){  
      install.packages('ggmap')  
    }  
    if (!('mapproj' %in% rownames(installed.packages()))){  
      install.packages('mapproj')  
    }  
    if (!('ROCR' %in% rownames(installed.packages()))){  
      install.packages('ROCR')  
    }  
    if (!('RODBC' %in% rownames(installed.packages()))){  
      install.packages('RODBC')  
    }  
    ```  
  
### <a name="install-required-packages-on-the-server"></a>Instalar los paquetes necesarios en el servidor  

  
1.  En el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , abra RGui.exe como administrador.  Si instaló SQL Server R Services usando los valores predeterminados, RGui.exe puede encontrarse en C:\Archivos de programa\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).  
  
    O bien, si instaló otro entorno de R en el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como RStudio), puede usar la consola de R para ejecutar los comandos.  
  
2.  En un símbolo del sistema de R, ejecute los siguientes comandos de R:  
  
    ```  
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])  
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1]) 
    ```  
  
**Notas:**  
  
-   Este ejemplo usa la función grep de R para buscar el vector de rutas de acceso disponibles y buscarlo en "Archivos de programa". Para obtener más información, consulte [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep).   
  
-   Si cree que los paquetes ya están instalados, use la función de R `installed.packages()` para revisar la lista de los paquetes instalados.  
  
-   En el cliente, puede instalar en una biblioteca de usuario si no puede escribir en la biblioteca principal en Archivos de programa. Sin embargo, cuando instala paquetes en el equipo con SQL Server, debe instalarlos en la biblioteca predeterminada usada por SQL Server R Services. No use una biblioteca de usuario. Para más información, consulte [Installing New R Packages on SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md) (Instalación de paquetes nuevos de R en SQL Server).
      

## <a name="3-run-powershell-script-runsqlrwalkthroughps1"></a>3. Ejecutar el script RunSQL_R_Walkthrough.ps1 de PowerShell  

Puede ejecutar este script de PowerShell en el equipo donde compilará la solución, por ejemplo, el equipo donde desarrollará y probará el código de R. Este equipo debe ser capaz de conectarse al equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el protocolo de canalizaciones con nombre.  
  
El script realiza estas acciones:  
  
-   Comprueba si el cliente nativo de SQL y las utilidades de línea de comandos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están instalados. La herramienta de línea de comandos es necesaria para ejecutar la [Utilidad bcp](../../tools/bcp-utility.md), que se usa para la carga masiva rápida de datos en tablas SQL.    
-   Se conecta a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ejecuta algunos scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] que configuran la base de datos y crean las tablas del modelo y los datos.    
-   Ejecuta un script de SQL para crear varios procedimientos almacenados.    
-   Carga los datos que descargó anteriormente en la tabla nyctaxi_sample.    
-   Vuelve a escribir los argumentos en el archivo de script de R para usar el nombre de la base de datos que especifique. 

### <a name="to-run-the-script"></a>Para ejecutar el script
  
1.  Abra una línea de comandos de PowerShell como administrador.    
  
2.  Navegue hasta la carpeta donde descargó los scripts y escriba el nombre del script como se muestra. Presione ENTRAR.  
  
    ```  
    .\RunSQL_R_Walkthrough.ps1  
    ```  
  
3.  Se le pedirá que especifique para cada uno de los siguientes parámetros:  
  
    - El nombre de la base de datos que quiere crear. 
      Por ejemplo, puede escribir **Tutorial** o **Taxi**  
    - Las credenciales con las que ejecutará el script. Hay dos opciones:
        + Escriba el nombre de un inicio de sesión de SQL con privilegios CREATE DATABASE y proporcione la contraseña de SQL en un símbolo del sistema posterior.
        + Presione ENTRAR sin escribir ningún nombre para usar su propia identidad de Windows y escriba su contraseña de Windows en el símbolo del sistema protegido. PowerShell no permite escribir un nombre de usuario de Windows distinto. 

          Si no especifica un usuario válido, el script usará, de manera predeterminada, la autenticación de Windows integrada.  
  
    -   La ruta de acceso completa al archivo csv que desea cargar en la base de datos  
  
        El script debe descargar el archivo y cargar los datos en la base de datos automáticamente, pero si se produce un error, siempre puede cargar los datos manualmente.  
  
4.  Pulse ENTRAR para ejecutar el script.  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 
 Si surgen problemas, puede llevar a cabo manualmente todos los pasos o algunos de ellos; para eso, use las líneas del script de PowerShell como ejemplos. 
 

### <a name="the-powershell-script-didnt-download-the-data"></a>El script de PowerShell no descargó los datos
  
Para descargar manualmente los datos, haga clic con el botón derecho en el siguiente vínculo y seleccione **Guardar destino como**.  
  
[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)  
  
Tome nota de la ruta de acceso al archivo de datos descargados y el nombre de archivo donde se guardaron los datos. Necesitará la ruta de acceso para cargar los datos a la tabla mediante **bcp**.  
  
### <a name="i-was-unable-to-download-the-data"></a>No pude descargar los datos
El archivo de datos es grande. Use un equipo con una conexión a Internet relativamente buena o es posible que se agote el tiempo de espera de la descarga.  

  
### <a name="could-not-connect-or-script-failed"></a>No se pudo conectar o hubo un error en el script  
  
+ Compruebe la ortografía del nombre de la instancia. 
+ Compruebe la cadena de conexión completa.    
+ Dependiendo de los requisitos de la red, es posible que el nombre de instancia requiera la calificación con uno o más nombres de subred.  Por ejemplo, si MISERVIDOR no funciona, inténtelo con miservidor.subred.miempresa.com.
  
### <a name="network-error-or-protocol-not-found"></a>Error de red o no se encontró el protocolo  
  
+ Compruebe que la instancia admite conexiones remotas.    
+ Compruebe que el usuario especificado de SQL puede conectarse remotamente a la base de datos y que las canalizaciones con nombre están habilitadas en la instancia.    
+ Compruebe los permisos de la cuenta. Es posible que la cuenta que especificó no tenga los permisos para crear una nueva base de datos y cargar los datos.  

### <a name="bcp-did-not-run"></a>No se ejecutó bcp  

+ Compruebe que la [Utilidad bcp](../../tools/bcp-utility.md) esté disponible en el equipo. Puede ejecutar bcp desde una ventana de PowerShell o desde un símbolo del sistema de Windows.
+ Si recibe un error, agregue la ubicación de la utilidad bcp en la variable de entorno del sistema PATH y vuelva a intentarlo.  

### <a name="the-table-schema-was-created-but-there-is-no-data-in-the-table"></a>Se creó el esquema de tabla pero no hay datos en la tabla

Si el resto del script se ejecutó sin problemas, puede cargar los datos manualmente en la tabla llamando a **bcp** desde la línea de comandos, de la siguiente manera:  


 
**Con un inicio de sesión de SQL**
    
~~~~ 
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password  
~~~~  
  
**Con la autenticación de Windows**  

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T 
~~~~ 
  
  
+ La palabra clave **in** especifica la dirección del movimiento de los datos.  
+ El argumento **-f** requiere que especifique la ruta de acceso completa de un archivo de formato. Se requiere un archivo de formato si usa la opción **in**.
+ Use los argumentos **-U** y **-P** si ejecuta bcp con un inicio de sesión de SQL.
+ Use el argumento **-T** si usa la autenticación integrada de Windows. 

  
### <a name="how-can-i-run-the-script-without-prompts"></a>¿Cómo puedo ejecutar el script sin mensajes?  
  
Puede especificar todos los parámetros en una sola línea de comandos, usando valores específicos para su entorno. 
  
```  
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>  
```  
  
Por ejemplo, para ejecutar el script con un inicio de sesión de SQL:  
  
```  
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv  
```  
  
En el ejemplo, se realizan las tareas siguientes:  
  
-   Se conecta a la instancia y la base de datos especificadas mediante las credenciales de *SqlUserName*.  
-   Obtiene los datos del archivo *C:\temp\nyctaxi1pct.csv*.  
-   Carga los datos en la tabla *dbo.nyctaxi_sample*, en la base de datos *MyDB* en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el nombre *MyServer*.  

### <a name="the-data-loaded-but-it-contains-duplicates"></a>Los datos se cargan, pero contienen duplicados

Si hay una tabla existente y presenta el esquema correcto, bcp seguirá ejecutándose, pero insertará una nueva copia de los datos en lugar de sobrescribir los datos existentes. Esto provocará datos duplicados.  Asegúrese de truncar las tablas existentes antes de volver a ejecutar el script.

## <a name="what-the-download-includes"></a>Qué incluye la descarga

Cuando descarga los archivos desde el repositorio de GitHub, obtendrá lo siguiente:
+ Datos en formato CSV
+ Un script de PowerShell para preparar el entorno
+ Un archivo de formato XML para importar los datos a SQL Server con bcp
+ Varios scripts T-SQL
+ Todo el código de R que necesita para ejecutar este tutorial

### <a name="training-and-scoring-data"></a>Datos de entrenamiento y puntuación  
Los datos son una muestra representativa del conjunto de datos de taxis de Nueva York, que contiene los registros de más de 173 millones de carreras individuales en 2013, incluidas las tarifas y las propinas pagadas por cada carrera.  Para obtener más información sobre cómo se recopilaron originalmente los datos y cómo puede obtener el conjunto de datos completo, consulte  
[http://chriswhong.com/open-data/foil_nyc_taxi/](http://chriswhong.com/open-data/foil_nyc_taxi/).  
  
Para que sea más fácil trabajar con los datos, el equipo de ciencia de datos de Microsoft redujo el tamaño del muestreo para obtener solo un 1 % de los datos.  Estos datos se han compartido en un contenedor de almacenamiento de blobs público en Azure, en formato .CSV. Los datos de origen están un archivo sin comprimir, ligeramente por debajo de 350MB.  
 
### <a name="files"></a>Archivos

 
+ **RunSQL_R_Walkthrough.ps1** Ejecutará primero este script, con PowerShell. Llama a los scripts de SQL para cargar datos en la base de datos.  
    
+ **taxiimportfmt.xml** Un archivo de definición de formato que usa la utilidad BCP para cargar datos en la base de datos.
      
+ **RSQL_R_Walkthrough.R** Este es el script básico de R que se usará en el resto de las lecciones para realizar el análisis de datos y el modelado. Proporciona todo el código de R que necesita para explorar datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , generar el modelo de clasificación y crear trazados.   
  
### <a name="sql-scripts"></a>Scripts de SQL  
Este script de PowerShell ejecuta varios scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el servidor. La siguiente tabla enumera los archivos de script de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Nombre de archivo del script de SQL|Lo que hace|  
|------------------------|----------------|  
|create-db-tb-upload-data.sql|Crea la base de datos y dos tablas:<br /><br /> *nyctaxi_sample*: la tabla que almacena los datos de entrenamiento, la muestra de un 1 % del conjunto de datos NYC Taxi. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta.<br /><br /> *nyc_taxi_models*: una tabla vacía que se va a usar más adelante para guardar el modelo de clasificación entrenado.|  
|PredictTipBatchMode.sql|Crea un procedimiento almacenado que llama a un modelo entrenado para predecir las etiquetas para las nuevas observaciones. Acepta una consulta como su parámetro de entrada.|  
|PredictTipSingleMode.sql|Crea un procedimiento almacenado que llama a un modelo de clasificación entrenado para predecir las etiquetas para las nuevas observaciones. Las variables de las nuevas observaciones se pasan como parámetros en línea.|  
|PersistModel.sql|Crea un procedimiento almacenado que ayuda a almacenar la representación binaria del modelo de clasificación en una tabla en la base de datos.|  
|fnCalculateDistance.sql|Crea una función de SQL con valores escalares que calcula la distancia directa entre las ubicaciones de origen y destino.|  
|fnEngineerFeatures.sql|Crea una función de SQL con valores de tabla que crea características para entrenar el modelo de clasificación|  
  
Todas las consultas SQL que se usan en este tutorial se han probado y se pueden usar tal cual en el código de R. Pero si quiere experimentar más o desarrollar su propia solución mediante consultas SQL, se recomienda usar un entorno de desarrollo como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para probar y ajustar las consultas en primer lugar, antes de agregarlas al código de R.  
  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Ver y explorar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lección anterior  
[Tutorial integral de ciencia de datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
  
  
