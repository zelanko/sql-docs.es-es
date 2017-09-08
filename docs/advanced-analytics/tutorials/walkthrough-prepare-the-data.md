---
title: Preparar los datos de uso de PowerShell (tutorial) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 65fd41d4-c94e-4929-a24a-20e792a86579
caps.latest.revision: 30
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e1d85684da36ef69caf9dfa39f155a320def37b5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="prepare-the-data-using-powershell-walkthrough"></a>Preparar los datos de uso de PowerShell (tutorial)

Llegados a este punto, debe tener instalado uno de los siguientes:

+ SQL Server 2016 R Services
+ SQL Server de 2017 Machine Learning Services, con el lenguaje R habilitado

En esta lección, descargue los datos, los paquetes de R y los scripts de R usados en el tutorial desde un repositorio de Github. Puede descargar todo el contenido mediante un script de PowerShell para su comodidad.

También debe instalar algunos paquetes de R adicionales, en el servidor y en la estación de trabajo de R. Se describen los pasos.

A continuación, utilizar un segundo script de PowerShell, RunSQL_R_Walkthrough.ps1, para configurar la base de datos que se usa para modelar y puntuación. Que el script realiza una carga masiva de los datos en la base de datos especifique y, a continuación, crea algunas funciones SQL y procedimientos almacenados que simplifican las tareas de ciencia de datos.

Comencemos!

## <a name="1-download-the-data-and-scripts"></a>1. Descargar los datos y las secuencias de comandos

Se ha proporcionado todo el código necesario en un repositorio de GitHub. Puede usar un script de PowerShell para crear una copia local de los archivos.

1.  En el equipo cliente de ciencia de datos, abra un símbolo del sistema de Windows PowerShell como administrador.

2.  Para asegurarse de que puede ejecutar el script descargado sin errores, ejecute este comando. Permite scripts de manera temporal sin cambiar los valores predeterminados del sistema.

    ```
    Set-ExecutionPolicy Unrestricted -Scope Process -Force
    ```
      
3.  Ejecute el siguiente comando de PowerShell para descargar los archivos de script en un directorio local. Si no especifica un directorio diferente, de forma predeterminada la carpeta `C:\tempR` se crea y todos los archivos guardados ahí.
  
    ```
    $source = 'https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/RSQL/Download_Scripts_R_Walkthrough.ps1'  
    $ps1_dest = "$pwd\Download_Scripts_R_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_R_Walkthrough.ps1 –DestDir 'C:\tempR'
    ```
  
    Si quiere guardar los archivos en un directorio diferente, edite los valores del parámetro *DestDir* y especifique una carpeta diferente en el equipo. Si escribe un nombre de carpeta no existe, la secuencia de comandos de PowerShell crea la carpeta automáticamente.
  
4.  La descarga puede tardar un rato. Una vez finalizada, la consola de comandos de Windows PowerShell debe tener un aspecto similar al siguiente:
  
    ![Después de la finalización del script de PowerShell](media/rsql-e2e-psscriptresults.PNG "Después de la finalización del script de PowerShell")
  
5.  En la consola de PowerShell, puede ejecutar el comando `ls` para ver una lista de los archivos descargados en *DestDir*.  Para obtener una descripción de los archivos, consulte [qué se incluye](#What-the-Download-Includes).

## <a name="2-install-required-r-packages"></a>2. Instalar paquetes de R necesarios

Este tutorial requiere algunas bibliotecas de R que no se instalan de forma predeterminada como parte de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Debe instalar los paquetes en el cliente donde desarrollar la solución y, en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo donde se implementa la solución.

### <a name="install-required-packages-on-the-client"></a>Instalar los paquetes necesarios en el cliente

El script de R que descargó incluye los comandos para descargar e instalar estos paquetes.

1. En su entorno de R, abra el archivo de script, RSQL_R_Walkthrough.R.

2. Resalte y ejecute estas líneas.
    
    ```
    # Install required R libraries, if they are not already installed.
    if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
    if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
    if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
    if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
    ```
    
    Algunos paquetes instalan paquetes necesarios. En general, se necesitan unos 32 paquetes.

### <a name="install-required-packages-on-the-server"></a>Instalar los paquetes necesarios en el servidor

Hay muchas maneras diferentes que puede instalar paquetes en SQL Server. Por ejemplo, SQL Server proporciona un [administración del paquete](../r/installing-and-managing-r-packages.md) característica que permite a los administradores de base de datos crea un repositorio de paquetes y asigna los derechos para instalar sus propios paquetes de usuario. Sin embargo, si es administrador en el equipo, puede instalar nuevos paquetes con R, siempre y cuando se instala en la biblioteca correcta.

> [!NOTE]
> En el servidor, **no** instalar en una biblioteca de usuario incluso si se le solicita. Si instala en una biblioteca de usuario, la instancia de SQL Server no se puede encontrar o ejecutar los paquetes. Para más información, consulte [Installing New R Packages on SQL Server](../r/install-additional-r-packages-on-sql-server.md)(Instalación de paquetes nuevos de R en SQL Server).

1. En el equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra RGui.exe **como administrador**.  Si instaló SQL Server R Services usando los valores predeterminados, RGui.exe puede encontrarse en C:\Archivos de programa\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).

2.  En un símbolo del sistema de R, ejecute los siguientes comandos de R:
  
    ```
    install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
    ```

    - Este ejemplo usa la función grep de R para buscar el vector de rutas de acceso disponibles y buscarlo en "Archivos de programa". Para obtener más información, consulte [http://www.rdocumentation.org/packages/base/functions/grep](http://www.rdocumentation.org/packages/base/functions/grep).

    - Si cree que ya están instalados los paquetes, compruebe la lista de paquetes instalados ejecutando `installed.packages()`.

## <a name="3-prepare-the-environment-using-runsqlrwalkthroughps1"></a>3. Preparar el entorno con RunSQL_R_Walkthrough.ps1

Junto con los archivos de datos, scripts de R y scripts de T-SQL, la descarga incluyen el script de PowerShell `RunSQL_R_Walkthrough.ps1`. El script realiza estas acciones:

- Comprueba si el cliente nativo de SQL y las utilidades de línea de comandos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están instalados. Se necesitan las herramientas de línea de comandos para ejecutar la [Utilidad bcp](../../tools/bcp-utility.md), que se usa para la carga masiva rápida de datos en tablas SQL.

- Se conecta a la instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ejecuta algunos scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] que configuran la base de datos y crean las tablas del modelo y los datos.

- Ejecuta un script de SQL para crear varios procedimientos almacenados.

- Carga los datos que descargó anteriormente en una tabla denominada `nyctaxi_sample`.

- Vuelve a escribir los argumentos en el archivo de script de R para usar el nombre de la base de datos que especifique.

Debe ejecutar este script en el equipo donde se compila la solución: por ejemplo, el equipo portátil donde desarrollar y probar el código de R. Este equipo, que denominaremos el cliente de ciencia de datos, debe poder conectarse al equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el protocolo de canalizaciones con nombre.

1. Abra una línea de comandos de PowerShell **como administrador**.
  
2.  Navegue hasta la carpeta donde descargó los scripts y escriba el nombre del script como se muestra. Presione ENTRAR.

    ```
    .\RunSQL_R_Walkthrough.ps1
    ```
  
3.  Se le solicitará a cada uno de los siguientes parámetros:
  
    **Nombre del servidor de base de datos**: el nombre de la instancia de SQL Server donde está instalado servicios o los servicios de R de aprendizaje de máquina.

    Dependiendo de los requisitos de la red, es posible que el nombre de instancia requiera la calificación con uno o más nombres de subred.  Por ejemplo, si MISERVIDOR no funciona, inténtelo con miservidor.subred.miempresa.com.
    
    **Nombre de la base de datos que quiere crear**: por ejemplo, puede escribir **Tutorial** o **Taxi**.

    **Nombre de usuario**: proporcione una cuenta que tenga privilegios de acceso a las bases de datos. Hay dos opciones:
    
    + Escriba el nombre de un inicio de sesión de SQL con privilegios CREATE DATABASE y proporcione la contraseña de SQL en un símbolo del sistema posterior.
    + Presione ENTRAR sin escribir ningún nombre para usar su propia identidad de Windows y escriba su contraseña de Windows en el símbolo del sistema protegido. PowerShell no permite escribir un nombre de usuario de Windows distinto.
    + Si no especifica un usuario válido, la secuencia de comandos predeterminado mediante la autenticación integrada de Windows.
    
      > [!WARNING]
      > Cuando utiliza el símbolo del sistema en el script de PowerShell para proporcionar sus credenciales, se escribe la contraseña en el archivo de script actualizado en texto sin formato. Edite el archivo para quitar las credenciales inmediatamente después de crear los objetos de R necesarios.
      
    **Ruta de acceso al archivo .csv**: proporcione la ruta de acceso completa al archivo de datos. La ruta de acceso y el nombre de archivo predeterminados son `C:\tempR\nyctaxi1pct.csv1`.
  
4.  Pulse ENTRAR para ejecutar el script.

    El script debería descargar el archivo y cargar los datos en la base de datos de manera automática. Esto puede tardar unos minutos. Observe los mensajes de estado indicados en la ventana de PowerShell.
      
    Si la importación masiva o cualquier paso produce un error, puede cargar los datos manualmente como se describe en el [solución de problemas](#bkmk_Troubleshooting) sección.

**Resultados (realización correcta)**

```
Execution successful
Completed registering all stored procedures used in this walkthrough.
This step (registering all stored procedures) takes 0.39 seconds.
Plug in the database server name, database name, user name and password into the R script file
This step (plugging in database information) takes 0.48 seconds.
```

Haga clic en este vínculo para saltar a la siguiente lección: [ver y explorar los datos mediante SQL](/walkthrough-view-and-explore-the-data.md)

## <a name="bkmk_Troubleshooting"></a>Solucionar problemas

Si tiene problemas con la secuencia de comandos de PowerShell, puede ejecutar todos o cualquiera de los pasos manualmente, utilizando las líneas de la secuencia de comandos de PowerShell como ejemplos. Esta sección enumeran algunos problemas comunes y soluciones alternativas.

### <a name="powershell-script-didnt-download-the-data"></a>El script de PowerShell no ha descargado los datos

Para descargar manualmente los datos, haga clic con el botón derecho en el siguiente vínculo y seleccione **Guardar destino como**.

[http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv](http://getgoing.blob.core.windows.net/public/nyctaxi1pct.csv)

Tome nota de la ruta de acceso al archivo de datos descargados y el nombre de archivo donde se guardaron los datos. Se necesita la ruta de acceso completa para cargar los datos a la tabla mediante **bcp**.

### <a name="unable-to-download-the-data"></a>No se pueden descargar los datos

El archivo de datos es grande. Debe usar un equipo que tenga una conexión a Internet relativamente buena, o la descarga, es posible que el tiempo de espera.

### <a name="could-not-connect-or-script-failed"></a>No se pudo conectar o hubo un error en el script

Es posible que reciba este error al ejecutar uno de los scripts: *Error relacionado con la red o específico de instancia al establecer conexión con el servidor SQL Server*.

+ Compruebe la ortografía del nombre de la instancia.
+ Compruebe la cadena de conexión completa.
+ Dependiendo de los requisitos de la red, es posible que el nombre de instancia requiera la calificación con uno o más nombres de subred.  Por ejemplo, si MISERVIDOR no funciona, inténtelo con miservidor.subred.miempresa.com.
+ Compruebe si el Firewall de Windows permite conexiones con SQL Server.
+ Intente registrar el servidor y asegúrese de que permite conexiones remotas.
+ Si usa una instancia con nombre, habilite SQL Browser para facilitar las conexiones.

### <a name="network-error-or-protocol-not-found"></a>Error de red o no se encontró el protocolo

+ Compruebe que la instancia admite conexiones remotas.
+ Compruebe que el usuario de SQL especificado puede conectarse remotamente a la base de datos.
+ Habilite las canalizaciones con nombre en la instancia.
+ Compruebe los permisos de la cuenta. Es posible que la cuenta que especificó no tenga los permisos para crear una nueva base de datos y cargar los datos.

### <a name="bcp-did-not-run"></a>No se ejecutó bcp

+ Compruebe que la [Utilidad bcp](../../tools/bcp-utility.md) esté disponible en el equipo. Puede ejecutar **bcp** desde una ventana de PowerShell o desde un símbolo del sistema de Windows.
+ Si recibe un error, agregue la ubicación de la utilidad **bcp** en la variable de entorno del sistema PATH y vuelva a intentarlo.

### <a name="the-table-schema-was-created-but-the-table-has-no-data"></a>Se ha creado el esquema de tabla pero no hay datos en la tabla

Si el resto del script se ejecutó sin problemas, puede cargar los datos manualmente en la tabla llamando a **bcp** desde la línea de comandos, de la siguiente manera:

#### <a name="using-a-sql-login"></a>Con un inicio de sesión de SQL

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -U <SQL login> -P <password>
~~~~

#### <a name="using-windows-authentication"></a>Con la autenticación de Windows

~~~~
bcp TutorialDB.dbo.nyctaxi_sample in c:\tempR\nyctaxi1pct.csv -t ',' -S rtestserver.contoso.com -f C:\tempR\taxiimportfmt.xml -F 2 -C "RAW" -b 200000 -T
~~~~

+ El `in` palabra clave especifica la dirección del movimiento de datos.
+ El argumento  **-f** requiere que especifique la ruta de acceso completa de un archivo de formato. Se requiere un archivo de formato si usa la opción **in** .
+ Use los argumentos **-U** y **-P** si ejecuta bcp con un inicio de sesión de SQL.
+ Use el argumento **-T** si usa la autenticación integrada de Windows.

Si el script no carga los datos, compruebe la sintaxis y asegúrese de que el nombre del servidor especificado para la red es correcto. Por ejemplo, no olvide incluir las subredes y el nombre del equipo si se va a conectar a una instancia con nombre. Compruebe que el inicio de sesión tiene la capacidad para realizar la carga masiva.

### <a name="i-want-to-run-the-script-without-prompts"></a>Quiero ejecutar el script sin mensajes

Mediante esta plantilla, puede especificar todos los parámetros en una sola línea de comandos con los valores específicos de su entorno.

```
.\RunSQL_R_Walkthrough.ps1 -server <server address> -dbname <new db name> -u <user name> -p <password> -csvfilepath <path to csv file>
```

En el ejemplo siguiente se ejecuta el script mediante un inicio de sesión de SQL:

```
.\RunSQL_R_Walkthrough.ps1 -server MyServer.subnet.domain.com -dbname MyDB –u SqlUserName –p SqlUsersPassword -csvfilepath C:\temp\nyctaxi1pct.csv
```

-   Se conecta a la instancia y la base de datos especificadas mediante las credenciales de *SqlUserName*.
-   Obtiene los datos del archivo *C:\temp\nyctaxi1pct.csv*.
-   Carga los datos en la tabla *dbo.nyctaxi_sample*, en la base de datos *MyDB* en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el nombre *MyServer*.

### <a name="the-data-loaded-but-it-contains-duplicates"></a>Los datos se cargan, pero contienen duplicados

Si la base de datos contiene una tabla existente del mismo nombre y el mismo esquema, **bcp** inserta una nueva copia de los datos en lugar de sobrescritura de los datos existentes.

Para evitar la duplicación de datos, asegúrese de truncar las tablas existentes antes de volver a ejecutar el script.

## <a name="whats-included-in-the-sample"></a>¿Qué se incluye en el ejemplo

Al descargar los archivos desde el repositorio de GitHub, obtendrá el siguiente:

+ Datos en formato CSV; vea [de entrenamiento y puntuación datos](#bkmk_data) para obtener más información
+ Un script de PowerShell para preparar el entorno
+ Un archivo de formato XML para importar los datos a SQL Server con bcp
+ Varios scripts T-SQL
+ Todo el código de R que necesita para ejecutar este tutorial

### <a name="bkmk_data"></a>Entrenamiento y de datos de puntuación

Los datos son una muestra representativa del conjunto de datos de taxis de Nueva York, que contiene los registros de más de 173 millones de carreras individuales en 2013, incluidas las tarifas y las propinas pagadas por cada carrera. Para que sea más fácil trabajar con los datos, el equipo de ciencia de datos de Microsoft redujo el tamaño del muestreo para obtener solo un 1 % de los datos.  Estos datos se han compartido en un contenedor de almacenamiento de blobs público en Azure, en formato .CSV. Los datos de origen están un archivo sin comprimir, ligeramente por debajo de 350MB.

+ Conjunto de datos público: [NYC Taxi y Limousine Comisión] (http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)

+ [Generar modelos de aprendizaje automático de Azure en el conjunto de datos de Nueva York Taxi] (https://blogs.technet.microsoft.com/machinelearning/2015/04/02/building-azure-ml-models-on-the-nyc-taxi-dataset/.

### <a name="powershell-and-r-script-files"></a>Archivos de script de PowerShell y R

+ **RunSQL_R_Walkthrough.ps1** ejecutar este script en primer lugar, con PowerShell. Llama a los scripts de SQL para cargar datos en la base de datos.

+ **taxiimportfmt.xml** Un archivo de definición de formato que usa la utilidad BCP para cargar datos en la base de datos.

+ **RSQL_R_Walkthrough.R** este es el script de R de núcleo que se utiliza en el resto de las lecciones de realizar el análisis de datos y modelado. Proporciona todo el código de R que necesita para explorar datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , generar el modelo de clasificación y crear trazados.

### <a name="t-sql-script-files"></a>Archivos de script de T-SQL

El script de PowerShell ejecuta varias [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos en la instancia de SQL Server. La siguiente tabla se recogen los [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos y lo que hacen.

|Nombre de archivo del script de SQL|Description|
|------------------------|----------------|
|create-db-tb-upload-data.sql|Crea la base de datos y dos tablas:<br /><br /> *nyctaxi_sample*: la tabla que almacena los datos de entrenamiento, la muestra de un 1 % del conjunto de datos NYC Taxi. Un índice de almacén de columnas agrupado se agrega a la tabla para mejorar el rendimiento de almacenamiento y de consulta.<br /><br /> *nyc_taxi_models*: una tabla vacía que se va a usar más adelante para guardar el modelo de clasificación entrenado.|
|PredictTipBatchMode.sql|Crea un procedimiento almacenado que llama a un modelo entrenado para predecir las etiquetas para las nuevas observaciones. Acepta una consulta como su parámetro de entrada.|
|PredictTipSingleMode.sql|Crea un procedimiento almacenado que llama a un modelo de clasificación entrenado para predecir las etiquetas para las nuevas observaciones. Las variables de las nuevas observaciones se pasan como parámetros en línea.|
|PersistModel.sql|Crea un procedimiento almacenado que ayuda a almacenar la representación binaria del modelo de clasificación en una tabla en la base de datos.|
|fnCalculateDistance.sql|Crea una función de SQL con valores escalares que calcula la distancia directa entre las ubicaciones de origen y destino.|
|fnEngineerFeatures.sql|Crea una función de SQL con valores de tabla que crea características para entrenar el modelo de clasificación|

Las consultas de T-SQL que se utilizan en este tutorial se han comprobado y se pueden ejecutar como-está en el código de R. Pero si quiere experimentar más o desarrollar su propia solución, se recomienda usar un entorno de desarrollo de SQL dedicado para probar y ajustar las consultas en primer lugar, antes de agregarlas al código de R.

+ La [extensión mssql](https://code.visualstudio.com/docs/languages/tsql) para [Visual Studio Code](https://code.visualstudio.com/) es un entorno gratuito y ligero para ejecutar consultas que también admite la mayoría de las tareas de desarrollo de base de datos.
+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) es una herramienta eficaz pero gratuita que se proporciona para el desarrollo y la administración de bases de datos de SQL Server.

## <a name="next-lesson"></a>Lección siguiente

[Ver y explorar los datos mediante R y SQL](/walkthrough-view-and-explore-the-data.md)

## <a name="previous-lesson"></a>Lección anterior

[Tutorial de ciencia de datos to-end para R y SQL Server](/walkthrough-data-science-end-to-end-walkthrough.md)

[Requisitos previos para el tutorial de ciencia de datos](walkthrough-prerequisites-for-data-science-walkthroughs.md)

