---
title: Crear un repositorio de paquete de R local mediante miniCRAN - SQL Server Machine Learning Services
description: Use miniCran para detectar, ensamblar e instalar las dependencias de paquetes de R en un único paquete consolidado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 83d73bb9d075825472cda96a7dcd54e25549de5e
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140630"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>Crear un repositorio de paquetes de R local mediante miniCRAN
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) paquete, creado por [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html), identifica y descarga los paquetes y dependencias en una sola carpeta, que puede copiar a otros equipos para la instalación de paquetes de R sin conexión.

Como entrada, especifique uno o varios paquetes. **miniCRAN** lee el árbol de dependencias para estos paquetes de forma recursiva y descarga solo los paquetes indicados y sus dependencias de CRAN o repositorios similar.

Como salida, **miniCRAN** crea un repositorio sea coherente internamente que consta de los paquetes seleccionados y todas las dependencias necesarias. A continuación, puede mover este repositorio local al servidor y continuar para instalar los paquetes sin conexión a internet.

> [!NOTE]
> Los usuarios experimentados de R a menudo buscan la lista de los paquetes dependientes en el archivo de descripción para el paquete descargado. Sin embargo, los paquetes enumerados en **importaciones** podría tener dependencias de segundo nivel. Por este motivo, se recomienda **miniCRAN** para ensamblar la colección completa de los paquetes necesarios.

## <a name="why-create-a-local-repository"></a>¿Por qué crear un repositorio local

El objetivo de crear un repositorio de paquetes local es proporcionar una ubicación única que un administrador del servidor u otros usuarios de la organización pueden usar para instalar nuevos paquetes de R en un servidor, especialmente uno que no tiene acceso a internet. Después de crear el repositorio, puede modificarla agregando nuevos paquetes o actualizar la versión de los paquetes existentes.

Repositorios de paquetes son útiles en estos escenarios:

- **Seguridad**: Muchos usuarios de R están acostumbrados a descargar e instalar nuevos paquetes de R a voluntad, desde CRAN o uno de sus sitios de réplica. Sin embargo, por motivos de seguridad, los servidores de producción que ejecutan [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] normalmente no tiene conectividad a internet.

- **Instalación sin conexión sea más fácil**: Para instalar el paquete en un servidor sin conexión requiere que también descargar todas las dependencias de paquete, Using miniCRAN resulta más fácil obtener todas las dependencias en el formato correcto.

    Mediante el uso de miniCRAN, puede evitar errores de dependencia del paquete al preparar los paquetes se instalan con el [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción.

- **Mejor administración de versión**: En un entorno multiusuario, existen buenas razones para evitar la instalación sin restricciones de varias versiones de paquete en el servidor. Usar un repositorio local para proporcionar un conjunto coherente de los paquetes para su uso por los analistas. 

> [!TIP]
> También puede usar miniCRAN para preparar los paquetes para su uso en Azure Machine Learning. Para obtener más información, consulte este blog: [Uso de miniCRAN en Azure Machine Learning por Michele Usuelli](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>Instalar miniCRAN

El **miniCRAN** propio paquete depende de 18 otros paquetes CRAN, entre los que es el **RCurl** paquete, que tiene una dependencia del sistema en el **curl desarrollo** paquete. De forma similar, empaquetar **XML** tiene una dependencia en **libxml2 desarrollo**. Para resolver las dependencias, se recomienda compilar el repositorio local inicialmente en un equipo con acceso completo a internet. 

Ejecute los siguientes comandos en un equipo con un base R y herramientas de R y conexión a internet. Se supone que se trata de *no* el equipo de SQL Server. El siguiente comando instala el **miniCRAN** paquete y el requerido **igraph** paquete. En este ejemplo se comprueba si el paquete ya está instalado, pero puede omitir el if instrucciones e instalar los paquetes directamente.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>Establecer el reflejo de CRAN y la instantánea MRAN

Especifique un sitio de réplica para usar al obtener los paquetes. Por ejemplo, podría utilizar el sitio MRAN o cualquier otro sitio en la región que contiene los paquetes que necesita. Si se produce un error en la descarga, pruebe a otro sitio de réplica.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>Cree una carpeta local

Cree una carpeta local, como `C:\mylocalrepo` donde se almacenarán los paquetes recopilados. Si se repite a menudo, probablemente debería usar un nombre más descriptivo, como "miniCRANZooPackages" o "miniCRANMyRPackagev2".

Especifique la carpeta que el repositorio local. Sintaxis de R usa una barra diagonal para los nombres de ruta de acceso, que es el opuesto de convenciones de Windows.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>Agregar paquetes al repositorio local

Después de **miniCRAN** se instala y carga, cree una lista que especifica los paquetes adicionales que desea descargar.

Hacer **no** agregar dependencias a esta lista inicial. El **igraph** paquete utilizado por **miniCRAN** genera la lista de dependencias para usted. Para obtener más información sobre cómo usar el gráfico de dependencias generado, vea [mediante miniCRAN para identificar las dependencias del paquete](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html).

1. Agregar paquetes de destino, "zoo" y "forecast" a una variable.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. También puede trazar el gráfico de dependencias, pero puede ser informativa.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. Cree el repositorio local. No olvide cambiar la versión de R si es necesario para la versión instalada en su instancia de SQL Server. Versión 3.2.2 está activado SQL Server 2016, versión 3.3 en SQL Server 2017. Si realizó una actualización de componentes, su versión podría ser más reciente. Para obtener más información, consulte [obtener R y Python información del paquete](../package-management/installed-package-information.md).

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   De esta información, el paquete de miniCRAN crea la estructura de carpetas que necesita para copiar los paquetes a la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] más adelante.

En este momento debe tener una carpeta que contiene los paquetes que necesita, y los paquetes adicionales que eran necesarios. La ruta de acceso debe ser similar a este ejemplo: C:\mylocalrepo\bin\windows\contrib\3.3 y deben contener una colección de los paquetes comprimidos. No se descomprima los paquetes o cambiar el nombre de los archivos.

Opcionalmente, ejecute el siguiente código para enumerar los paquetes del repositorio local de miniCRAN.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>Agregar paquetes a la biblioteca de instancia

Una vez que un repositorio local con los paquetes que necesita, mueva el repositorio de paquetes en el equipo de SQL Server. El siguiente procedimiento describe cómo instalar los paquetes mediante herramientas de R.

1. Copie la carpeta que contiene el repositorio de miniCRAN en su totalidad en el servidor donde va a instalar los paquetes. Normalmente, la carpeta tiene esta estructura: miniCRAN raíz > bin > windows > contrib > versión > todos los paquetes. En los ejemplos siguientes, se supone una carpeta en la unidad raíz: 

2. Abra una herramienta de R asociada a la instancia (por ejemplo, podría usar Rgui.exe). Haga clic en **ejecutar como administrador** para permitir que la herramienta realizar actualizaciones en el sistema.

    - Para SQL Server 2017, es la ubicación del archivo RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`.

    - Para SQL Server 2016, es la ubicación del archivo RGUI `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`.

3. Obtener la ruta de acceso de la biblioteca de la instancia y agréguelo a la lista de rutas de acceso de biblioteca. En SQL Server 2017, la ruta de acceso es similar al ejemplo siguiente.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. Especifique la nueva ubicación en el servidor donde haya copiado el **miniCRAN** repositorio, como `server_repo`.

    En este ejemplo, asumimos que copió del repositorio en una carpeta temporal en el servidor.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. Puesto que está trabajando en una nueva área de trabajo de R en el servidor, también debe proporcionar la lista de paquetes para instalar.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. Instale los paquetes, que proporciona la ruta de acceso a la copia local del repositorio de miniCRAN.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. Desde la biblioteca de la instancia, puede ver los paquetes instalados con un comando similar al siguiente:

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>Vea también

+ [Obtención de información del paquete](../package-management/installed-package-information.md)
+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
