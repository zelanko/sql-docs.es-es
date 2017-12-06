---
title: Instalar paquetes de R adicionales en SQL Server | Documentos de Microsoft
ms.date: 11/15/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: f8d20c5b5b687a6d9d94cd97605f294cead27215
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar paquetes de R adicionales en SQL Server

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server donde está habilitado el aprendizaje automático.

> [!IMPORTANT]
> El proceso para agregar nuevos paquetes varía según la versión de SQL Server que se está ejecutando y las herramientas que está utilizando. 

**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] y  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]
[!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="overview-of-package-installation-process"></a>Información general del proceso de instalación de paquete

1.  Determinar si hay una versión de Windows del paquete: [obtener la versión de paquete correcto y formato](#packageVersion)

2.  Si el servidor no tiene acceso a internet, descargue los archivos binarios de antemano: [archivos zip de descarga](#bkmk_zipPreparation)

    Asegúrese de comprobar las dependencias de paquete y obtener todos los paquetes relacionados que podrían ser necesarios durante la instalación. Para preparar una colección de paquetes y sus dependencias, se recomienda la [miniCRAN paquete](#bkmk_packageDependencies).

    Si se producen errores de descarga o la instalación, intente un sitio de réplica diferente.

3.  Cómo instalar el paquete depende de si el servidor tiene acceso a internet y de la versión de SQL Server. Los procesos recomendados son los siguientes:

    **Instalación del paquete de SQL Server 2016**
    
    1. Los científicos de datos proporciona los paquetes necesarios para un proyecto o equipo. Use [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar las colecciones de paquetes con sus dependencias.

    2. El Administrador de base de datos instala los paquetes en la biblioteca de instancia mediante herramientas de R.

    **Instalación del paquete para SQL Server 2017**

    1. El Administrador de base de datos permite la administración de paquetes en la instancia y agrega los usuarios a los nuevos roles de administración del paquete.

    2. Los científicos de datos proporciona los paquetes necesarios para un proyecto o equipo. Use [miniCRAN](create-a-local-package-repository-using-minicran.md) para preparar las colecciones de paquetes con sus dependencias.

    3. El paquete se carga en la instancia de SQL Server, utilizando la instrucción crear biblioteca externa.
    
    4. Después de que el paquete se ha agregado a la instancia, cualquier usuario con los permisos adecuados puede instalar los paquetes a la base de datos donde se ejecutan los scripts de R, mediante una llamada a código de R desde `sp_execute_external_script`.
    
    5. Los usuarios con los permisos adecuados pueden instalar o buscar paquetes desde un cliente remoto de R, mediante la nueva función de RevoScaleR para administración de paquetes.

## <a name="install-new-packages"></a>Instalar nuevos paquetes

En esta sección se proporcionan procedimientos detallados para escenarios de instalación del paquete de claves. Elegir el mejor método, dependiendo de:

- La versión de SQL Server que usa

- Si es el único propietario de la instancia, o intenta administrar paquetes de varias personas mediante roles de base de datos.

- Si está instalando un paquete o varios paquetes con dependencias

**Use Administración de paquetes de SQL Server**

Si la instancia es compatible con características de administración de paquetes, puede usar T-SQL o herramientas de R convencionales.

-  Paquete de carga un R a un servidor SQL donde obtener acceso administración de paquetes y el paquete basada en roles está habilitado. Un usuario, a continuación, instala el paquete con código T-SQL.

    [Instalar paquetes mediante crear biblioteca externa](#bkmk_sqlInstall)

- Utilice a un cliente remoto de R para agregar nuevos paquetes a un servidor. Requiere que SQL Server de 2017. Administración de paquetes se debe haber habilitado en el servidor. 

    [Usar R para instalar paquetes en un servidor cuando se habilita la administración de paquetes](#bkmk_rAddPackage)

- Preparar una biblioteca de paquete para su uso con crear biblioteca externa contiene varios paquetes junto con sus dependencias.

    [Instalar varios paquetes desde un repositorio de miniCRAN](#bkmk_minicran)

**Usar herramientas de R convencionales**

Si está utilizando una versión anterior de SQL Server R services, siga estas instrucciones para instalar paquetes con herramientas de R convencionales. Opcionalmente, utilice miniCRAN para preparar una colección de paquetes para la instalación.

-  Instalar un paquete de R en la biblioteca de instancia predeterminada con herramientas de R. Requiere acceso administrativo.

    [Instalar paquetes en la biblioteca de instancia con herramientas de R](#bkmk_rInstall)

- Crear una colección compartida de paquetes para admitir facilita la instalación de varios paquetes y sus dependencias.

    [Crear un repositorio de paquetes mediante miniCRAN](create-a-local-package-repository-using-minicran.md)

### <a name="bkmk_sqlInstall"></a>Instalar paquetes mediante las herramientas de SQL Server

1. Asegúrese de que se ha habilitado la característica de administración de biblioteca externa de 2017 de SQL Server en la instancia.

    [Cómo habilitar o deshabilitar la administración de paquetes](r-package-how-to-enable-or-disable.md)

2. Conectarse al servidor mediante una cuenta que tenga permisos para instalar nuevos paquetes, mediante uno de los roles de base de datos compatibles se describe en este tema: [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md)

3.  Copie el archivo comprimido que contiene el paquete de R que se va a instalar en una carpeta en el equipo del servidor, como la **usuarios** o **documentos** carpeta. No se puede agregar un paquete desde una unidad de red o desde una carpeta en el equipo cliente. Si ha utilizado miniCRAN para crear un repositorio de paquetes, copie el repositorio de paquetes en su totalidad en cualquier carpeta local en el servidor: es decir, no en una unidad de red.

    Si no tiene acceso a las carpetas en el servidor, puede pasar el contenido del paquete en formato binario. Vea [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) para obtener un ejemplo.

4.  En la base de datos donde desea usar el paquete, ejecute el [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción.

    En este ejemplo, se supone que la cuenta tiene permiso para cargar nuevos paquetes en el servidor e instalarlas a **compartido** ámbito en la base de datos.

    La siguiente instrucción agrega la versión de lanzamiento de la [zoo](https://cran.r-project.org/web/packages/zoo/index.html) paquete en el contexto de base de datos actual, desde un recurso compartido de archivos local.

    ```SQL
    CREATE EXTERNAL LIBRARY zoo
    FROM (CONTENT = 'C:\Temp\RPackages\zoo_1.8-0.zip')
    WITH (LANGUAGE = 'R');
    ```

    Si se conecta con una cuenta que es un propietario de la base de datos (miembro del rol dbo), el paquete debe ponerse a disposición en **compartido** ámbito: es decir, se puede instalar cualquier usuario que sea miembro de los `rpkgs-users` rol.

    Si va a cargar el paquete con una cuenta que puede tener acceso a solo **privada** ámbito, el paquete se puede instalar sólo por parte del usuario.

4.  Para instalar el paquete en la biblioteca predeterminada R usada por la instancia, ejecute el R `library()` comando dentro de la sp_execute_external_script de procedimiento almacenado.

    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # load the binaries in zoo
    library(zoo)'
    ```

    Si se realiza correctamente, el **mensajes** ventana debería notificar un mensaje como "paquete"zoo"desempaquetado correctamente y comprueban las sumas de MD5". Si un requisitos de software ya está instalado, el proceso de instalación, a continuación, se adjunta y carga el paquete necesario.

    > [!NOTE]
    > Si un paquete necesario no está disponible, se devuelve un error: "no hay ningún paquete denominado \<required_package\>". 
    > 
    > Para evitar errores, se recomienda que compruebe las dependencias de paquetes con antelación, o use miniCRAN para recopilar todos los paquetes necesarios en un solo archivo comprimido antes de ejecutar `CREATE EXTERNAL LIBRARY`.

### <a name="bkmk_rAddPackage"></a>Usar R para instalar paquetes en un servidor cuando se habilita la administración de paquetes

Si ya ha habilitado la administración de paquetes en la instancia, puede instalar nuevos paquetes de R desde un cliente remoto de R, utilizando las funciones de RevoScaleR para administración de paquetes.

1. Antes de empezar, asegúrese de que se cumplen estas condiciones:

    + Utilice la versión más reciente del cliente de R de Microsoft, que incluye actualizaciones para RevoScale.
    + Se ha habilitado la administración de paquetes en la instancia y en la base de datos.
    + Tener permiso para uno de los roles de administración de base de datos.

2. Enumerar los paquetes que desea instalar en una variable de cadena.

    ```R
    packageList <- c("e1071")
    ```
    
3. Definir una cadena de conexión a la instancia y la base de datos donde está habilitada la administración de paquetes y usar la cadena de conexión para crear un contexto de proceso de SQL Server.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

4. Llame a `rxInstallPackages` y pase el contexto de proceso y la variable de cadena que contiene los nombres de paquete.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Si se requieren paquetes dependientes, también se descargarán.
    
    En este ejemplo, porque no se especificó el propietario del paquete y el ámbito, el paquete se instala con las credenciales del usuario que realiza la conexión y los paquetes se instalan con el ámbito predeterminado para ese usuario.

### <a name="bkmk_rInstall"></a>Instalar paquetes en la biblioteca de instancia con herramientas de R

Puede usar herramientas de R para instalar nuevos paquetes en SQL Server 2016 y 2017 de SQL Server. Sin embargo, debe ser un administrador para hacerlo.

1.  Si el servidor no tiene acceso a internet, descargue los paquetes antes de tiempo.

    Se recomienda que utilice un repositorio de paquetes para preparar las colecciones de paquetes sin conexión. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

2.  Navegue hasta la carpeta en el servidor donde se instalan las bibliotecas de R para la instancia.

    > [!IMPORTANT] 
    > Asegúrese de instalar paquetes en la biblioteca predeterminada que está asociada a la instancia actual. Nunca instale paquetes en un directorio de usuario. Para obtener instrucciones sobre cómo localizar la biblioteca predeterminada, vea [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md).

    Para cada instancia donde se ejecuta un paquete, instale una copia independiente del paquete. Los paquetes no se pueden compartir entre instancias.

4.  Abra un símbolo del sistema de R como administrador.

    Por ejemplo, si usa el símbolo del sistema de Windows, navegue al directorio donde se encuentran los archivos RTerm.Exe o RGui.exe. 

    **Instancia predeterminada**

    2017 de SQL Server:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **Instancia con nombre**

    2017 de SQL Server:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

5.  Ejecute el comando R `install.packages` para instalar el paquete.

    La sintaxis depende de si se obtiene el paquete desde Internet o desde un archivo comprimido local. 

    **Instalar el paquete mediante una conexión a internet**

    Por ejemplo, la instrucción siguiente instala el paquete de e1071 populares. Las comillas dobles siempre se necesitan para el nombre del paquete.

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    Cuando se le pida un sitio de réplica, seleccione cualquier sitio que es conveniente para su ubicación.

    Si el paquete de destino depende de otros paquetes, descarga las dependencias automáticamente el instalador de R y los instala automáticamente.

    **Instalar el paquete de forma manual o en un equipo sin acceso a Internet**

    Si el paquete que quiere instalar tiene dependencias, obtenga los paquetes necesarios antes de tiempo y agréguelos a la carpeta con otros archivos de paquete comprimidos. Consulte la [sugerencias de instalación](#bkmk_tips) sección para obtener ayuda sobre cómo preparar los paquetes.

    En el símbolo del sistema de R, escriba el comando siguiente para especificar la ruta de acceso y el nombre del paquete que se va a instalar:

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Este comando extrae un único paquete de R de su archivo comprimido local, siempre que haya guardado la copia en el directorio `C:\Temp\Downloaded packages`e instala el paquete (con sus dependencias) en la biblioteca de R en el equipo local.

### <a name="bkmk_minicran"></a>Instalar varios paquetes desde un repositorio de miniCRAN

El proceso general de instalación de paquetes de un repositorio miniCRAN es similar a la instalación de un paquete de un único archivo comprimido. Sin embargo, en lugar de cargar un paquete individual en formato comprimido, el repositorio de miniCRAN contiene el paquete de destino, así como los paquetes necesarios relacionados.

1.  Prepare el repositorio de miniCRAN y, a continuación, copie el archivo comprimido a una carpeta local en el servidor.

2.  Si usas T-SQL, un administrador ejecuta la instrucción T-SQL `CREATE EXTERNAL LIBRARY` para cargar la recopilación del paquete comprimido en la base de datos.

    Por ejemplo, la siguiente instrucción hace referencia a un repositorio de miniCRAN que contiene el paquete de randomForest y sus dependencias.

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

3. Para instalar los paquetes para su uso con SQL Server, ejecute el comando siguiente como parte del código de R en un procedimiento almacenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    Si se realiza correctamente, el **mensajes** ventana debería notificar un mensaje como "paquete 'randomForest' desempaquetado correctamente y las sumas de MD5 comprueban" y "Finished encadenadas ejecución".

## <a name="package-installation-tips"></a>Sugerencias de instalación de paquete

Esta sección proporciona sugerencias ordenadas y código de ejemplo relacionados con la instalación del paquete de R en SQL Server. 

###  <a name="packageVersion"></a>Obtener la versión de paquete correcto y formato

Puede obtener paquetes de R de varios orígenes, aunque los más conocidos son CRAN y Bioconductor. El sitio oficial del lenguaje R (<https://www.r-project.org/>) recoge muchos de estos recursos. Número de paquetes se publica en GitHub, donde puede obtener el código fuente. Sin embargo, se podrán haber recibido paquetes de R desarrollados por algún miembro de su empresa.

Independientemente del origen, debe asegurarse de que el paquete que se va a instalar tiene un formato binario para la plataforma Windows. En caso contrario, no se puede ejecutar el paquete descargado en el entorno de SQL Server.

Antes de descargar, también debe comprobar si el paquete es compatible con la versión de R que se ejecuta en SQL Server.

### <a name="bkmk_zipPreparation"></a>Descargar el paquete como archivo comprimido

Para la instalación en un servidor sin acceso a internet, descargue una copia del paquete en el formato de un archivo comprimido para la instalación sin conexión. Descomprima el paquete.

Por ejemplo, el siguiente procedimiento describe ahora para obtener la versión correcta de la [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) paquete desde Bioconductor, suponiendo que el equipo tiene acceso a internet.

1.  En la lista de **archivos de paquetes** , busque la versión **binaria de Windows** .

2.  Haga clic en el vínculo a la. Archivo ZIP y seleccione **Guardar destino como**.

3.  Vaya a la carpeta local donde se almacenan los paquetes comprimidos y haga clic en **guardar**.

Este proceso crea una copia local del paquete. A continuación, puede instalar el paquete, o copiar el paquete comprimido en un servidor que no tiene acceso a internet.

Para obtener más información sobre el contenido del formato de archivo zip y cómo crear un paquete de R, se recomienda este tutorial, que puede descargar en formato PDF desde el sitio de proyecto de R: [crear paquetes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).

### <a name="bkmk_packageDependencies"></a>Obtener las dependencias de paquetes

Paquetes de R con frecuencia dependen de varios otros paquetes, algunos de los cuales podrían no estar disponibles en la biblioteca de R predeterminada utilizada por la instancia. O bien, en ocasiones, un paquete requiere una versión diferente de un paquete dependiente que ya está instalado.

Si necesita instalar varios paquetes o desea asegurarse de que todas las personas de su organización obtienen el tipo de paquete correcto y la versión, recomendamos que use el paquete miniCRAN para crear un repositorio local que se pueden compartir entre varios usuarios o equipos. Para obtener más información, consulte [crear un repositorio de paquete local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="permissions"></a>Permissions

Si es un usuario experto de R, es posible que acostumbrados a la instalación de paquetes de la línea de comandos sin permisos especiales o sin necesidad de descargarlos de antemano. Sin embargo, la mayoría de los servidores no tiene una conexión a internet. Además, el acceso a recursos compartidos de archivos o almacenamiento podría estar restringido.

Esta sección describe el nivel de permisos necesarios para instalar paquetes en SQL Server 2016 y SQl Server 2017 diferente. Instalación puede realizarse mediante herramientas de R o SQL Server, pero el proceso y los permisos son ligeramente distintas.

-   SQL Server 2016

    En esta versión, solo un administrador en el equipo puede instalar paquetes a la ubicación deseada. Use las herramientas de R estándar para instalar paquetes, pero debe ejecutar como administrador y utilizar las herramientas de R asociadas a la instancia.

-   SQL Server 2017

    Esta versión proporciona nuevas características que permiten que un administrador de base de datos delegar la instalación del paquete a los usuarios. El DBA debe habilitar las características de administración de paquetes en por instancia. Después de habilita esta característica, el DBA puede usar roles de base de datos para conceder a usuarios individuales la capacidad para instalar paquetes según sea necesario, o para compartir paquetes por base de datos.

    Para obtener más información, consulte [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md).


> [!IMPORTANT]
> 
> Los usuarios experimentados de R están acostumbrados a la instalación de paquetes en una biblioteca de usuario y, a continuación, hacer referencia al paquete en dicha carpeta como parte de la solución en R, especificando una ruta de acceso de archivo. Sin embargo, esta práctica no se admite en SQL Server. Para obtener más información y soluciones alternativas, consulte [cómo usar paquetes de bibliotecas de usuario](packages-installed-in-user-libraries.md).

### <a name="comparing-package-management-methods"></a>Comparación de métodos de administración de paquetes

En esta sección se compara los métodos de instalación de paquete disponibles y se enumera algunas consideraciones adicionales y sugerencias para ayudarle a determinar una estrategia de administración e instalación de paquetes apropiada.

#### <a name="using-sql-server-package-management-features"></a>Uso de características de administración de paquetes de SQL Server

Si habilita la administración de paquetes, instale un paquete para una base de datos. Si necesita usar un paquete en todas las bases de datos donde está habilitada la secuencia de comandos de R, deberá instalarlo en cada base de datos.

Sin embargo, dado que SQL Server administra la información sobre el usuario que tiene derecho a utilizar los paquetes, es más fácil copiar información sobre los usuarios y los paquetes entre las bases de datos. También es fácil volver a generar un conjunto de paquetes de trabajo de un usuario o varios usuarios al restaurar una base de datos, o cuando se mueve entre instancias.

Usar T-SQL y las características de administración de paquetes en SQL Server 2017 es el método preferido siempre que haya varios usuarios de base de datos se instala o ejecuta paquetes de R.

Esta característica está disponible a partir 2017 de SQL Server.

#### <a name="using-r-tools-to-install-packages-for-the-sql-server-instance"></a>Con herramientas de R para instalar paquetes de la instancia de SQL Server

Si utiliza este método, los paquetes instalados para la instancia están disponibles en cualquier base de datos. Sin embargo, dado que los paquetes se instalan directamente en el sistema de archivos, deben administrarse fuera de SQL Server. Paquetes no pueden ser copia de seguridad o restaurar. Además, el Administrador de base de datos debe aprender a usar herramientas de R.

Sin embargo, esta solución es la más sencilla si es el único propietario de la base de datos.

#### <a name="managing-multiple-packages-and-multiple-versions-of-the-same-package"></a>Administración de varios paquetes y varias versiones del mismo paquete

Si necesita realizar la instalación sin conexión de paquetes de R, configurar un repositorio local usando [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) le permite compartir los paquetes y administrar las versiones disponibles para su uso por la organización.

#### <a name="establish-a-single-mirror-site-as-standard"></a>Establecer un sitio reflejado único como estándar

Si prefiere no tener que seleccionar un sitio reflejado cada vez que agregue un nuevo paquete, puede configurar el entorno de desarrollo de R para que use siempre el mismo repositorio. Para ello, edite el archivo de configuración global de R, **. Rprofile**y agregue la siguiente línea:

`options(repos=structure(c(CRAN="<mirror site URL>")))`

Reflejados de CRAN actuales se muestran en [este sitio](https://cran.r-project.org/mirrors.html).

Para obtener información detallada sobre las preferencias y otros archivos cargados al iniciarse el runtime de R, ejecute este comando desde una consola de R:`?Startup`

#### <a name="know-which-library-you-are-using-for-installation"></a>Saber qué biblioteca se usar para la instalación

Si previamente se ha modificado el entorno de R en el equipo, antes de instalar cualquier cosa, poner en pausa un momento y asegúrese de que la variable de entorno de R `.libPath` utiliza una sola ruta de acceso.

Esta ruta de acceso debe apuntar a la carpeta R_SERVICES para la instancia. Para obtener más información, consulte [paquetes de R instalados con SQL Server](installing-and-managing-r-packages.md).

#### <a name="side-by-side-installation-with-r-server"></a>Instalación en paralelo con R Server

Si ha instalado al servidor de aprendizaje de máquina de Microsoft (independiente) además de los servicios de aprendizaje de máquina de SQL Server, el equipo debe tener instalaciones independientes de R para cada, con los duplicados de todas las bibliotecas y herramientas de R.

> [!IMPORTANT]
> 
> Paquetes que se instalan en la biblioteca R_SERVER solo son utilizados por Microsoft R Server y no se pueden tener acceso a SQL Server.
> 
> Asegúrese de utilizar el `R_SERVICES` biblioteca al instalar los paquetes que desea usar en SQL Server.
