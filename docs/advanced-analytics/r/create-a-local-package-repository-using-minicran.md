---
title: Crear un repositorio de paquete local mediante miniCRAN | Documentos de Microsoft
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 1dd7e8f1a0054818849b3b9672a5df6286bdabce
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>Crear un repositorio de paquete local mediante miniCRAN

Hay dos maneras en que se pueden preparar los paquetes de R para la instalación en un servidor sin acceso a internet.

-   [Usar el paquete de miniCRAN para crear un solo repositorio local](#bkmk_miniCRAN)

    El [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) crea un repositorio coherente internamente que consta de los paquetes seleccionados desde repositorios de CRAN similar. El usuario especifica un conjunto de paquetes que desee y miniCRAN recursivamente lee el árbol de dependencias para estos paquetes y descarga solo los paquetes indicados y sus dependencias.

    A continuación, puede mover este repositorio local al servidor y continuar para instalar los paquetes sin usar internet.

-   [Descargar manualmente y copiar paquetes uno a uno](#bkmk_manual)

Este artículo describe cómo puede crear un repositorio de paquetes de R con ambos métodos, y recomienda el uso de la **miniCRAN** paquete.

## <a name="prepare-packages-using-minicran"></a>Preparar los paquetes mediante miniCRAN

El objetivo de crear un repositorio de paquetes local es proporcionar una única ubicación que un administrador del servidor u otros usuarios de la organización pueden utilizar para instalar nuevos paquetes de R en un servidor que no tiene acceso a internet.

El [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) del paquete de R se escribe por [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) para que resulten más fáciles de crear coherente, administrada por conjunto de paquetes de R de una organización. 

Hay muchas ventajas en el uso de miniCRAN para crear el repositorio:

-   **Seguridad**: R muchos usuarios están acostumbrados a descargar e instalar nuevos paquetes de R como desee, de CRAN o uno de sus sitios de réplica. Sin embargo, por motivos de seguridad, los servidores de producción que ejecutan [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] normalmente no tiene conectividad a internet.

-   **Instalación sin conexión más sencilla e**: para instalar el paquete en un servidor sin conexión requiere que también descargar todas las dependencias del paquete, mediante miniCRAN resulta más fácil obtener todas las dependencias en el formato correcto.

-   **Mejor administración de versión**: en un entorno multiusuario, hay buenos motivos para evitar la instalación sin restricciones de varias versiones de paquete en el servidor.

Después de crear el repositorio, puede modificar mediante la adición de nuevos paquetes o actualizar la versión de los paquetes existentes.

### <a name="step-1-install-the-minicran-package"></a>Paso 1. Instalar el paquete miniCRAN

Empiece por crear un repositorio de miniCRAN para usarlo como un origen. Debe crear este repositorio en un equipo que tenga acceso a internet.

1.  Instalar el paquete de miniCRAN y requerido **igraph** paquete.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>Paso 2. Definir un origen de paquete: un espejo CRAN, o una instantánea MRAN

1. Especifique un sitio de réplica a usar para la obtención de paquetes.

    ```R
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
    ```

2.  Indique una carpeta local donde se almacenarán los paquetes recopilados. No asigne un nombre a la miniCRAN carpeta; es posible que un nombre más descriptivo como "GeneticsPackages" o "ClientRPackages1.0.2".

    Asegúrese de crear la carpeta de antemano. Se produce un error si el `local_repo` carpeta no existe cuando se ejecuta el código de R más adelante.

    ```R
    local_repo <- "~/miniCRAN"
    ```

    El operador de tilde expansión devuelve una variable de entorno, con resultados equivalente a `Sys.getenv("R_USER")`.

### <a name="step-3-add-packages-to-the-repository"></a>Paso 3. Agregar paquetes en el repositorio

1.  Después de instalar miniCRAN, cree una lista que especifica los paquetes adicionales que desea descargar.

    No agregar dependencias a esta lista inicial; el **igraph** paquete que utiliza miniCRAN genera la lista de dependencias para usted. Para obtener más información sobre cómo usar este gráfico, consulte [con miniCRAN para identificar las dependencias del paquete](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

    El siguiente script de R muestra cómo obtener los paquetes de destino, "zoo" y "previsión".

    ```R
    pkgs_needed <- c("zoo", "forecast")

2. Optionally, plot the dependency graph, which can be informative and looks cool.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Cree el repositorio local. No olvide cambiar la versión de R si es necesario

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror)
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3")
    ```

    De esta información, el paquete miniCRAN crea la estructura de carpetas que necesita para copiar los paquetes a la [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] más tarde.

4. En este momento debe tener una carpeta que contiene los paquetes que sea necesario, y todos los paquetes que se necesitaban.

    Puede ejecutar el código siguiente para obtener una lista de los paquetes que se incluyen en el repositorio de miniCRAN.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE)
    head(pdb)
    pdb$Package
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>Paso 4. Use el repositorio para agregar paquetes de R a la biblioteca de instancia

Una vez haya creado el repositorio y agregar los paquetes que necesita, debe mover el repositorio de paquetes en el equipo servidor y asegúrese de que los paquetes de R se instalan en la biblioteca correcta para su uso desde SQL Server.

Según la versión de SQL Server, hay dos opciones para agregar nuevos paquetes a la biblioteca de R asociada a la instancia de SQL Server:

-   Instalar en la biblioteca de instancia mediante el repositorio de miniCRAN y herramientas de R.

-   Cargar paquetes de una base de datos de SQL e instalar paquetes en una base de cada base de datos, utilizando la instrucción crear biblioteca externa. Vea [instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md).

El siguiente procedimiento describe cómo instalar los paquetes con herramientas de R.

1.  Copie la carpeta que contiene el repositorio miniCRAN, en su totalidad, en el servidor donde vaya a instalar los paquetes.

2.  Abra un símbolo del sistema de R mediante la herramienta de R asociada a la instancia.

    - Para SQL Server 2017, la carpeta predeterminada es `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`.

    - Para SQL Server 2016, la carpeta predeterminada es `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`.

    - Para una instancia con nombre, la ruta de acceso predeterminada sería algo parecido a: `<instance_path>.RTEST/R_SERVICES/library`.

    -  Si ha instalado SQL Server en una unidad diferente, o ha realizado otros cambios en la ruta de instalación, asegúrese de introducir esos cambios también.

3.  Obtener la ruta de acceso de la biblioteca de instancia (en caso de que esté en un directorio de usuarios) y agregarlo a la lista de rutas de acceso de biblioteca.

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    Se debe devolver la ruta de acceso de instancia, "C:/programa archivos/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/biblioteca"

2.  Especifique la ubicación en el servidor donde haya copiado el repositorio de mininCRAN en `server_repo`.

    En este ejemplo, se supone que ha copiado el repositorio en la carpeta de usuario en el servidor.

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

3.  Puesto que está trabajando en una nueva área de trabajo de R en el servidor, también debe proporcionar la lista de paquetes que se va a instalar.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

4.  Instale los paquetes, mediante la ruta de acceso a la copia local del repositorio miniCRAN.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

5.  Ahora, ver los paquetes instalados.

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 
> En SQL Server 2017, se proporcionan funciones adicionales de la base de datos y las instrucciones de T-SQL para ayudar a los administradores del servidor administrar permisos a través de paquetes. El Administrador de base de datos puede poseer la tarea de instalación de paquetes, con R o T-SQL, si así lo desea. Sin embargo, el DBA también puede utilizar roles para conceder a los usuarios la capacidad para instalar sus propios paquetes. Para obtener más información, consulte [administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md).
> 
> En SQL Server 2016, un administrador del servidor debe instalar los paquetes del repositorio de miniCRAN en la biblioteca predeterminada utilizada por la instancia. Para ello, utilice las herramientas de R como se describe en el [sección anterior](#bkmk_Rtools).

## <a name="manually-download-single-packages"></a>Descargar manualmente los paquetes únicos

Si no desea usar miniCRAN, puede descargar manualmente los paquetes que necesita y sus dependencias. Para hacer esto requiere que sea un administrador o un único propietario de un servidor.

Después de descargar los paquetes, debe instalar los paquetes de R de la ubicación del archivo comprimido.

1.  Descargar los archivos zip de paquetes y guardarlos en una carpeta local

2.  Copie esta carpeta a la [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] equipo.

3.  Instale los paquetes en la biblioteca de la instancia de SQL Server.

> [!NOTE]
> Al usar herramientas de R para instalar paquetes, se instalan para la instancia como un todo. 
> 
> Si desea instalar el paquete en una base de datos y compartir el paquete con los usuarios con roles de base de datos, debe cargar la biblioteca mediante la instrucción crear biblioteca externa. Vea [instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md)

