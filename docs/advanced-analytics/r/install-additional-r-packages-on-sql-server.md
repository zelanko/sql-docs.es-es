---
title: Instalar paquetes de R adicionales en SQL Server | Documentos de Microsoft
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 530745918dfd4808694b401be55e40bac00f3cce
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar paquetes de R adicionales en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server donde está habilitado el aprendizaje automático.

**Se aplica a:** 
+ [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]
+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="prerequisites"></a>Requisitos previos

+ Determinar si hay una versión de Windows del paquete: [obtener la versión de paquete correcto y formato](#packageVersion)

+ Si el servidor no tiene acceso a internet, debe descargar los archivos binarios de Windows de antemano: [archivos zip de descarga](#bkmk_zipPreparation)

+ Identificar las dependencias del paquete. 

    - Si el servidor tiene acceso a internet, no es necesario preocuparse de las dependencias; todos los paquetes necesarios pueden instalarse automáticamente.

    - Si el servidor no **no** tener acceso a internet, primero debe identificar todas las dependencias y descargar los paquetes necesarios de antemano, en formato comprimido. Una manera sencilla de hacerlo es usar [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar una colección de paquetes con todas las dependencias. Este repositorio, a continuación, puede copiarse en el equipo del servidor.

+ Compruebe la compatibilidad de los paquetes. El paquete debe ser compatible con la versión de R que se ejecuta en SQL Server.

    Además, compruebe si el paquete (o todos los paquetes que requiere) contienen características que se bloquearía por SQL Server o por la directiva. Por ejemplo, algunos paquetes no resultan adecuadas para un entorno de SQL Server protegido. Estos paquetes pueden incluir los paquetes que tienen acceso a la red, que usan Java u otros marcos no suele usadas en un entorno de SQL Server o paquetes que requieren acceso al sistema de archivos con privilegios elevados.

+ Permissions

    Se requiere acceso administrativo al equipo que ejecuta SQL Server.

    Además, para ejecutar en SQL Server, paquetes deben instalarse en la biblioteca predeterminada que está asociada a la instancia actual. Para obtener instrucciones sobre cómo localizar la biblioteca predeterminada, vea [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md).
    
    Si es un usuario experto de R, es posible que acostumbrados a la instalación de paquetes de la línea de comandos sin permisos especiales o sin necesidad de descargarlos de antemano. Sin embargo, este método no funciona en SQL Server. En muchos casos SQL Server equipos no tienen una conexión a internet. Además, el acceso a archivos del servidor o un almacenamiento externo podría estar restringido. No se pueden tener acceso a los paquetes instalados en una biblioteca de usuario por runnign de trabajos de R en SQL Server. 

    Si no tiene acceso administrativo al equipo de SQL Server, busque un administrador de base de datos para ayudar con la instalación del paquete.

+ Para cada instancia que necesite usar el paquete, ejecutar la instalación por separado.

     Los paquetes no se pueden compartir entre instancias. Puede usar el mismo origen de archivo comprimido para instalar el paquete para instancias independientes, pero una copia independiente del paquete se agrega a cada biblioteca de instancia.

## <a name="install-packages"></a>Instalar paquetes

Esta sección proporciona los pasos de instalación del paquete para los siguientes escenarios:

+ [Instalar nuevos paquetes en un servidor con acceso a Internet](#bkmk_rInstall)
+ [Realizar una instalación sin conexión de paquetes en un servidor con **sin** acceso a internet](#bkmk_offlineInstall)
+ [Instalar paquetes en un contexto de proceso de SQL Server con RevoScaleR](#bkmk_rAddPackage)
+ [Instalar paquetes mediante la instrucción crear biblioteca externa](#bkmk_createlibrary) (SQL Server solo 2017; otras restricciones se aplican)

### <a name="bkmk_rInstall"></a>Instalación en línea con herramientas de R

Puede utilizar las herramientas estándar de R para instalar nuevos paquetes en una instancia de SQL Server 2016 o 2017 de SQL Server. Sin embargo, debe ser un administrador para hacerlo.

1.  Navegue hasta la carpeta en el servidor donde se instalan las bibliotecas de R para la instancia.

    > [!IMPORTANT] 
    > Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. Nunca instale paquetes en un directorio de usuario.

    Si no tiene los permisos necesarios, póngase en contacto con el Administrador de base de datos y proporcionar una lista de los paquetes que necesita.

2.  Abra un símbolo del sistema de R como administrador.

    Por ejemplo, si usa el símbolo del sistema de Windows, navegue al directorio donde se encuentran RTerm.Exe o RGui.exe. 

    **Instancia predeterminada**

    2017 de SQL Server:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Instancia con nombre**

    2017 de SQL Server:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

    Si ha utilizado el enlace para actualizar los componentes de aprendizaje automático, podría haber cambiado la ruta de acceso. Compruebe siempre la ruta de acceso de instancia antes de instalar nuevos paquetes. 

3.  Ejecute el comando R `install.packages` para instalar el paquete. Por ejemplo, la instrucción siguiente instala el paquete de e1071 populares. 

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    Las comillas dobles son necesarias para el nombre del paquete.

4. Cuando se le pida un sitio de réplica, seleccione cualquier sitio que es conveniente para su ubicación.

5. Si el paquete de destino depende de otros paquetes, descarga las dependencias automáticamente el instalador de R y los instala automáticamente.

> [!IMPORTANT]
> Para cada instancia que necesite usar el paquete, ejecutar la instalación por separado. Los paquetes no se pueden compartir entre instancias.

### <a name = "bkmk_offlineInstall"></a>Instalación sin conexión con herramientas de R 

Si el paquete que se va a instalar tiene dependencias, preparar **todos los** paquetes antelación requeridos.  Consulte la [sugerencias de instalación](#bkmk_tips) sección para obtener ayuda sobre cómo preparar los paquetes.

> [!IMPORTANT]
>  Siempre que se instalación paquetes en un servidor que no tenga acceso a internet, es fundamental que analizar dependencias completadas de antemano y asegúrese de que ha descargado todos los paquetes necesarios **antes de** comenzar la instalación. Se recomienda [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para este proceso. Este paquete de R toma una lista de paquetes que desea instalar, analiza las dependencias y obtiene todos los archivos comprimidos. miniCRAN, a continuación, crea un repositorio único que puede copiar en el equipo del servidor.
> 
> Para obtener más información, vea [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md)

1. Copie el paquete o en el repositorio en formato comprimido en un recurso compartido local o en otra ubicación que el servidor tiene acceso.

2.  Busque la carpeta en el servidor donde se instalan las bibliotecas de R para la instancia.

    Por ejemplo, si usa el símbolo del sistema de Windows, navegue al directorio donde se encuentran RTerm.Exe o RGui.exe.

    **Instancia predeterminada**

    2017 de SQL Server:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Instancia con nombre**

    2017 de SQL Server:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. Abra un símbolo del sistema de R como administrador.

4.  Ejecute el comando R `install.packages` y especifique el paquete o el nombre del repositorio y la ubicación de los archivos comprimidos.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrae el paquete de R `mynewpackage` de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`e instala el paquete en el equipo local. Si el paquete tiene dependencias, el instalador comprueba si los paquetes existentes en la biblioteca. Si ha creado un repositorio que incluye las dependencias, el programa de instalación instala los paquetes de fijas así.

    Si los paquetes necesarios no están presentes en la biblioteca de la instancia y no se encuentra en los archivos comprimidos, se produce un error en la instalación del paquete de destino.

### <a name="bkmk_rAddPackage"></a>Instalar paquetes de R en un servidor desde un cliente remoto de R

En versiones recientes de [R Server o servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server), RevoScaleR incluye funciones que admiten la instalación de nuevos paquetes de R en un contexto de proceso de SQL Server. 

1. Antes de empezar, asegúrese de que se cumplen estas condiciones:

    + El cliente tiene RevoScale 9.0.1 o una versión posterior.
    + Se ha instalado una versión equivalente de RevoScaleR en la instancia de SQL Server.
    + El [característica de administración de paquetes](..\r\r-package-how-to-enable-or-disable.md) se ha habilitado en la instancia.
    + Es miembro de un rol de base de datos que le permite instalar paquetes en un compartido o un contexto de prvate, en la instancia especificada y ddatabase.

2. Desde una línea de comandos de R, definir una cadena de conexión a la instancia y la base de datos y usar la cadena de conexión con el [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) constructor para crear un contexto de proceso de SQL Server.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Crear una lista de los paquetes que desea instalar y guardar la lista en una variable de cadena.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Llame a [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) y pase el contexto de proceso y la variable de cadena que contiene los nombres de paquete.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Si se requieren paquetes dependientes, también se instalan, suponiendo que está disponible una conexión a internet.
    
    En este ejemplo, porque no se especificó el propietario y el ámbito, se instalan paquetes, lo que con las credenciales del usuario que realiza la conexión, en el ámbito predeterminado para ese usuario.

### <a name="bkmk_createlibrary"></a>Usar un repositorio de miniCRAN y crear una biblioteca externa para instalar paquetes 

SQL Server 2017 proporciona nuevas características para instalar y administrar paquetes de R mediante T-SQL. Sin embargo, este proceso requiere que un paquete esté disponible como una variable local zip, en lugar de descargar de internet. La instrucción produce un error si todos los paquetes no están preparados de antemano.

CREAR una biblioteca externa se admite en las siguientes condiciones:

+ Va a instalar un único paquete no tiene dependencias
+ Va a instalar varios paquetes, o con dependencias y haber preparado todos los paquetes de antemano. 

**Pasos**

1.  Preparar el paquete en formato comprimido, o crear un repositorio de miniCRAN que contiene el paquete y sus dependencias.  

2. Copie el archivo comprimido o en el repositorio en una carpeta local en el servidor.

     > [!IMPORTANT]
     > El archivo que especifique como origen debe contener el paquete de destino, así como los paquetes necesarios relacionados.

3. Como administrador, ejecute la instrucción de T-SQL `CREATE EXTERNAL LIBRARY` para cargar la recopilación del paquete comprimido en la base de datos.

    Por ejemplo, la siguiente instrucción hace referencia a un repositorio de miniCRAN que contiene el paquete de randomForest y sus dependencias. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    No se puede usar un nombre arbitrario en la instrucción CREATE; el nombre de biblioteca externa debe tener el mismo nombre que se espera que se utilizará al cargar o el paquete de la llamada.

4. Instale el paquete o paquetes para su uso con SQL Server, mediante la ejecución de código dentro de un procedimiento almacenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    Si se realiza correctamente, el **mensajes** ventana debería notificar un mensaje como "paquete 'randomForest' desempaquetado correctamente y las sumas de MD5 comprueban" y "Finished encadenadas ejecución".

    Si se produce un error en la instalación, producirá un error en todos los paquetes de instalación y los intentos subsiguientes de paquete de instalación pueden también producirá un error, con este mensaje: 

    "Error en rxSqlPkgInstallPackages... No se pudo instalar paquetes: examine el registro para obtener más información"

## <a name="package-installation-tips-and-frequently-asked-questions-faq"></a>Sugerencias de instalación de paquete y las preguntas más frecuentes (P+F)

Esta sección proporciona sugerencias ordenadas y preguntas comunes relacionadas con la instalación del paquete de R en SQL Server.

###  <a name="packageVersion"></a>Obtener la versión de paquete correcto y formato

Puede obtener paquetes de R de varios orígenes, aunque los más conocidos son CRAN y Bioconductor. El sitio oficial del lenguaje R (<https://www.r-project.org/>) recoge muchos de estos recursos. Número de paquetes se publica en GitHub, donde puede obtener el código fuente. Sin embargo, se podrán haber recibido paquetes de R desarrollados por algún miembro de su empresa.

Independientemente del origen, debe asegurarse de que el paquete que se va a instalar tiene un formato binario para la plataforma Windows. En caso contrario, no se puede ejecutar el paquete descargado en el entorno de SQL Server.

### <a name="bkmk_zipPreparation"></a>Descargar el paquete como un archivo comprimido

Para la instalación en un servidor sin acceso a internet, debe descargar una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. Descomprima el paquete.

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta de la [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) paquete desde Bioconductor, suponiendo que el equipo tiene acceso a internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic en el vínculo a la. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **guardar**.

    Este proceso crea una copia local del paquete. Si recibe un error de descarga, pruebe a un sitio de réplica diferente.

4. Después de que se ha descargado el archivo de paquete, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a internet.

> [!TIP]
> Si por error instala el paquete en lugar de descargar los archivos binarios, también se guarda una copia del archivo zip descargado en el equipo. Ver los mensajes de estado tal y como se instala el paquete para determinar la ubicación del archivo. Puede copiar dicho archivo comprimido en el servidor que no tiene acceso a internet.
> Si descarga el paquete mediante este método, no se incluyen las dependencias del paquete. 

Para obtener más información sobre el contenido del formato de archivo zip y cómo crear un paquete de R, se recomienda este tutorial, que puede descargar en formato PDF desde el sitio de proyecto de R: [crear paquetes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).

### <a name="bkmk_packageDependencies"></a>Obtener las dependencias de paquetes

Paquetes de R con frecuencia dependen de varios otros paquetes, algunos de los cuales podrían no estar disponibles en la biblioteca de R predeterminada utilizada por la instancia. A veces, un paquete requiere una versión diferente de un paquete dependiente que ya está instalado.

Si necesita instalar varios paquetes o desea asegurarse de que todas las personas de su organización obtienen el tipo de paquete correcto y la versión, recomendamos que use la [miniCRAN](https://mran.microsoft.com/package/miniCRAN) paquete para crear un repositorio local que se pueden compartir entre varios usuarios o equipos. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="permissions"></a>Permissions

Esta sección describe el nivel de permisos necesarios para instalar paquetes en SQL Server 2016 y SQL Server 2017 diferente. Instalación puede realizarse mediante herramientas de R o SQL Server, pero el proceso y los permisos son ligeramente distintas.

-   SQL Server 2016

    En esta versión, solo un administrador en el equipo puede instalar paquetes a la ubicación deseada. Use las herramientas de R estándar para instalar paquetes, pero debe ejecutar como administrador y utilizar las herramientas de R asociadas a la instancia.

-   SQL Server 2017

    Si tiene acceso administrativo, puede instalar paquetes de forma toda la instancia mediante las herramientas de R.

    Si es un propietario de base de datos, puede instalar paquetes de R desde un cliente remoto, si se define una conexión y conectarse a la instancia con RxInSqlServer.
    
    Esta versión incluye nuevas características para admitir la administración de paquetes de R o Python por los administradores de base de datos en las próximas versiones. Para usar esta característica, un DBA en primer lugar debe habilitar las características de administración de paquetes en por instancia. Después de habilita esta característica, los usuarios individuales pueden instalar paquetes a una base de datos, dependiendo de su rol de base de datos. Para obtener más información, consulte [habilitar o deshabilitar la administración de paquetes de R para SQL Server](../r/r-package-how-to-enable-or-disable.md).

> [!IMPORTANT]
> 
> Los usuarios experimentados de R están acostumbrados a la instalación de paquetes en una biblioteca de usuario y, a continuación, hacer referencia al paquete en dicha carpeta como parte de la solución en R, especificando una ruta de acceso de archivo. Sin embargo, esta práctica no se admite en SQL Server. Para obtener más información y soluciones alternativas, consulte [cómo usar paquetes de bibliotecas de usuario](packages-installed-in-user-libraries.md).

### <a name="establish-a-single-mirror-site-as-standard"></a>Establecer un sitio reflejado único como estándar

Si prefiere no tener que seleccionar un sitio reflejado cada vez que agregue un nuevo paquete, puede configurar el entorno de desarrollo de R para que use siempre el mismo repositorio. Para ello, edite el archivo de configuración global de R, **. Rprofile**y agregue la siguiente línea:

`options(repos=structure(c(CRAN="<mirror site URL>")))`

Reflejados de CRAN actuales se muestran en [este sitio](https://cran.r-project.org/mirrors.html).

Para obtener información detallada sobre las preferencias y otros archivos cargados al iniciarse el runtime de R, ejecute este comando desde una consola de R:`?Startup`

### <a name="know-which-library-you-are-using-for-installation"></a>Saber qué biblioteca se usar para la instalación

Si previamente se ha modificado el entorno de R en el equipo, antes de instalar cualquier cosa, poner en pausa un momento y asegúrese de que la variable de entorno de R `.libPath` utiliza una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES para la instancia. Para obtener más información, consulte [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-r-server"></a>Instalación en paralelo con R Server

Si ha instalado al servidor de aprendizaje de máquina de Microsoft (independiente) además de los servicios de aprendizaje de máquina de SQL Server, el equipo debe tener instalaciones independientes de R para cada una, con los duplicados de todas las bibliotecas y herramientas de R.

> [!IMPORTANT]
> 
> Paquetes que se instalan en la biblioteca R_SERVER solo son utilizados por Microsoft R Server y no se pueden tener acceso a SQL Server.
> 
> Asegúrese de utilizar el `R_SERVICES` biblioteca al instalar los paquetes que desea usar en SQL Server.

### <a name="how-to-determine-which-packages-are-already-installed"></a>¿Cómo determinar qué paquetes ya están instalados?

 Vea [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md)