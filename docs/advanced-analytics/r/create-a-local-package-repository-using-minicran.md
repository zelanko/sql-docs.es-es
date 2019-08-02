---
title: Creación de un repositorio de paquetes de R local mediante miniCRAN
description: Use miniCran para detectar, ensamblar e instalar dependencias de paquetes de R en un único paquete consolidado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a2324ad662cad2c91bc6e002fd652fed73d8ab3d
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715762"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Creación de un repositorio de paquetes de R local mediante miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

paquete [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) , creado por [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica y descarga paquetes y dependencias en una sola carpeta, que se puede copiar en otros equipos para la instalación de paquetes de R sin conexión.

Como entrada, especifique uno o varios paquetes. **miniCRAN** Lee de forma recursiva el árbol de dependencias para estos paquetes y descarga solo los paquetes enumerados y sus dependencias de Cran o repositorios similares.

Como salida, **miniCRAN** crea un repositorio interno coherente que consta de los paquetes seleccionados y de todas las dependencias necesarias. Después, puede trasladar este repositorio local al servidor y continuar con la instalación de los paquetes sin conexión a Internet.

> [!NOTE]
> Los usuarios con experiencia en R suelen buscar la lista de paquetes dependientes en el archivo de Descripción del paquete descargado. Sin embargo, los paquetes enumerados en las importaciones pueden tener dependencias de segundo nivel. Por esta razón, se recomienda **miniCRAN** para ensamblar la colección completa de paquetes necesarios.

## <a name="why-create-a-local-repository"></a>Por qué crear un repositorio local

El objetivo de crear un repositorio de paquetes local es proporcionar una ubicación única que un administrador de servidor u otros usuarios de la organización pueden usar para instalar nuevos paquetes de R en un servidor, especialmente uno que no tenga acceso a Internet. Después de crear el repositorio, puede modificarlo agregando nuevos paquetes o actualizando la versión de los paquetes existentes.

Los repositorios de paquetes son útiles en estos escenarios:

- **Seguridad**: Muchos usuarios de R están acostumbrados a descargar e instalar nuevos paquetes de R en, desde CRAN o desde uno de sus sitios de reflejo. Sin embargo, por motivos de seguridad, los [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] servidores de producción que ejecutan normalmente no tienen conectividad a Internet.

- **Instalación sin conexión más fácil**: Para instalar el paquete en un servidor sin conexión, es necesario que también descargue todas las dependencias del paquete, con miniCRAN es más fácil obtener todas las dependencias en el formato correcto.

    Mediante miniCRAN, puede evitar errores de dependencia de paquetes al preparar los paquetes para la instalación con la instrucción [Create external library](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) .

- **Administración de versiones mejorada**: En un entorno multiusuario, existen buenas razones para evitar la instalación sin restricciones de varias versiones de paquetes en el servidor. Use un repositorio local para proporcionar un conjunto coherente de paquetes para su uso por parte de los analistas. 

> [!TIP]
> También puede usar miniCRAN para preparar los paquetes para su uso en Azure Machine Learning. Para obtener más información, consulte este blog: [Uso de miniCRAN en aprendizaje automático de Azure, por Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Instalación de miniCRAN

El propio paquete **miniCRAN** depende de otros 18 paquetes de Cran, entre los que se encuentra el paquete **RCurl** , que tiene una dependencia del sistema en el paquete **de rizo-desarrollo** . Del mismo modo, el paquete **XML** tiene una dependencia en **libxml2-desarrollo**. Para resolver las dependencias, se recomienda compilar el repositorio local inicialmente en una máquina con acceso a Internet completo. 

Ejecute los siguientes comandos en un equipo con una conexión base de R, R Tools y Internet. Se supone que *no* es su equipo SQL Server. Los siguientes comandos instalan el paquete **miniCRAN** y el paquete **igraph** necesario. En este ejemplo se comprueba si el paquete ya está instalado, pero se pueden omitir las instrucciones if e instalar los paquetes directamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Establecimiento de la instantánea CRAN y MRAN

Especifique un sitio reflejado que se usará para obtener paquetes. Por ejemplo, puede usar el sitio MRAN o cualquier otro sitio de su región que contenga los paquetes que necesite. Si se produce un error en la descarga, pruebe con otro sitio reflejado.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Crear una carpeta local

Cree una carpeta local, por ejemplo `C:\mylocalrepo` , en la que almacenar los paquetes recopilados. Si se repite con frecuencia, probablemente debería usar un nombre más descriptivo, como "miniCRANZooPackages" o "miniCRANMyRPackagev2".

Especifique la carpeta como repositorio local. La sintaxis de R usa una barra diagonal para los nombres de ruta de acceso, que es opuesto a las convenciones de Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Agregar paquetes al repositorio local

Una vez instalado y cargado **miniCRAN** , cree una lista que especifique los paquetes adicionales que desea descargar.

**No** agregue dependencias a esta lista inicial. El paquete **igraph** que usa **miniCRAN** genera la lista de dependencias. Para obtener más información sobre cómo usar el gráfico de dependencias generado, vea [uso de miniCRAN para identificar las dependencias de paquete](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Agregue paquetes de destino, "Zoo" y "Forecast" a una variable.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. Opcionalmente, trace el gráfico de dependencias, pero puede ser informativo.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Cree el repositorio local. Asegúrese de cambiar la versión de R si es necesario a la versión instalada en la instancia de SQL Server. La versión 3.2.2 está en SQL Server 2016, la versión 3,3 está en SQL Server 2017. Si ha realizado una actualización de componente, es posible que la versión sea más reciente. Para obtener más información, vea [obtener información de paquetes de R y Python](../package-management/installed-package-information.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   A partir de esta información, el paquete miniCRAN crea la estructura de carpetas que necesita para copiar los paquetes [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] a la versión más reciente.

En este punto, debe tener una carpeta que contenga los paquetes que necesita y los paquetes adicionales necesarios. La ruta de acceso debe ser similar a la de este ejemplo: C:\mylocalrepo\bin\windows\contrib\3.3 y debe contener una colección de paquetes comprimidos. No Descomprima los paquetes ni cambie el nombre de los archivos.

Opcionalmente, ejecute el siguiente código para enumerar los paquetes contenidos en el repositorio local de miniCRAN.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Agregar paquetes a la biblioteca de instancias

Una vez que tenga un repositorio local con los paquetes que necesita, mueva el repositorio de paquetes al SQL Server equipo. En el procedimiento siguiente se describe cómo instalar los paquetes mediante herramientas de R.

1. Copie la carpeta que contiene el repositorio de miniCRAN, en su totalidad, en el servidor donde va a instalar los paquetes. Normalmente, la carpeta tiene esta estructura: miniCRAN root > bin > Windows > distrib > version > All packages. En los ejemplos siguientes, se supone que hay una carpeta fuera de la unidad raíz: 

2. Abra una herramienta de R asociada a la instancia (por ejemplo, puede usar Rgui. exe). Haga clic con el botón secundario en **Ejecutar como administrador** para permitir que la herramienta realice actualizaciones en el sistema.

    - Por SQL Server 2017, la ubicación del archivo de RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`es.

    - Por SQL Server 2016, la ubicación del archivo para RGUI `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`es.

3. Obtenga la ruta de acceso de la biblioteca de instancias y agréguela a la lista de rutas de acceso de la biblioteca. En SQL Server 2017, la ruta de acceso es similar al ejemplo siguiente.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Especifique la nueva ubicación en el servidor donde copió el repositorio de **miniCRAN** , como `server_repo`.

    En este ejemplo, se supone que ha copiado el repositorio en una carpeta temporal del servidor.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Dado que está trabajando en un nuevo área de trabajo de R en el servidor, también debe proporcionar la lista de paquetes que se van a instalar.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. Instale los paquetes y proporcione la ruta de acceso a la copia local del repositorio de miniCRAN.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. Desde la biblioteca de instancias, puede ver los paquetes instalados con un comando similar al siguiente:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>Vea también

+ [Obtención de información del paquete](../package-management/installed-package-information.md)
+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
