---
title: Crear un repositorio de paquete local mediante miniCRAN | Documentos de Microsoft
ms.custom: 
ms.date: 03/30/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8af93b3e132290eef4b43da568b9381ff8e5a04
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>Crear un repositorio de paquete local mediante miniCRAN
En este tema, se describe cómo puede crear un repositorio del paquete de R local con el **miniCRAN** del paquete de R. 

Dado que las instancias de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] normalmente se encuentran en un servidor que no tiene conectividad a Internet, puede que no funcione el método estándar de instalación de paquetes de R (el comando de R `install.packages()`), ya que el instalador del paquete no puede tener acceso a CRAN u otros sitios de réplica.

Hay dos opciones para instalar paquetes desde un recurso compartido local o el repositorio:

+ Usar el paquete de miniCRAN para crear un repositorio local de los paquetes que necesita y después instalar desde este repositorio. En este tema se describe el método de miniCRAN.

+ Descargar los paquetes que necesite, y sus dependencias, como archivos zip, guardarlos en una carpeta local y después copiar esa carpeta en el equipo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Para obtener más información sobre el método de copia manual, consulte [Instalar paquetes adicionales en SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).


## <a name="step-1-install-minicran-and-download-packages"></a>Paso 1. Instalar miniCRAN y descargar los paquetes 


1. Instale el paquete de miniCRAN en un equipo que tenga acceso a Internet.

   ~~~~
   # Install miniCRAN and igraph

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. Descargue o instale los paquetes que necesite en este equipo mediante el siguiente script de R. Esto creará la estructura de carpetas que necesita para copiar los paquetes en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] más adelante.

   ~~~~
   # List the packages to get. Do not specify dependencies.
   pkgs_needed <- c("ggplot2", "ggdendro")
   # Plot the dependency graph 
   plot(makeDepGraph(pkgs_needed)) 
   
   # Create the local repo 
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror) 
   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.2") 

   # List local packages 
   pdb <- as.data.frame( 
     pkgAvail(local_repo, type = "win.binary", Rversion = "3.2"),  
     stringsAsFactors = FALSE) 
   head(pdb) 
   pdb$Package 
   pdb[, c("Package", "Version", "License")] 
   ~~~~


## <a name="step-2-copy-the-minicran-repository-to-the-sql-server-computer"></a>Paso 2. Copiar el repositorio de miniCRAN en el equipo con SQL Server 

Copie el repositorio de miniCRAN en la biblioteca R_SERVICES en la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

+ Para SQL Server 2016, la carpeta predeterminada es `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library1`.
+ Para SQL Server 2017, la carpeta predeterminada es `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library1`.

Si ha instalado R Services con una instancia con nombre, asegúrese de incluir el nombre de la instancia en la ruta de acceso, para asegurarse de que las bibliotecas se instalan en la instancia correcta. Por ejemplo, si la instancia con nombre es RTEST02, la ruta de acceso predeterminada para la instancia con nombre sería: `C:\Program Files\Microsoft SQL Server\MSSQL13.RTEST02\R_SERVICES\library`.

Si ha instalado SQL Server en una unidad diferente, o ha realizado otros cambios en la ruta de instalación, asegúrese de introducir esos cambios también.

## <a name="step-3-install-the-packages-on-sql-server-using-the-minicran-repository"></a>Paso 3. Instalar los paquetes en SQL Server con el repositorio de miniCRAN

En el equipo [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], abra una línea de comandos de R o RGUI como administrador. 
  
> [!TIP]
> Es posible que tenga varias bibliotecas de R en el equipo; por tanto, para asegurarse de que esos paquetes se instalan en la instancia correcta, use la copia de RGUI o RTerm que se instala con la instancia específica en que quiere instalar los paquetes.
  
Cuando se le pida especificar un repositorio, seleccione la carpeta que contiene los archivos que acaba de copiar; es decir, el repositorio local de miniCRAN.

   ~~~~
   # Run this R code as administrator on the SQL Server computer 
   pkgs_needed <- c("ggplot2", "ggdendro") 
   local_repo  <- "~/miniCRAN" 

   # OPTIONAL: If you are not running R from the instance library as recommended, you must specify the path
   #   .libPaths()[1] 
   # "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library " 
   # lib <- .libPaths()[1]
   
   install.packages(pkgs_needed,  
                    repos = file.path("file://", normalizePath(local_repo, winslash = "/")), 
                    lib = lib, 
                    type = "win.binary", 
                    dependencies = TRUE 
                    ) 
   installed.packages() 
   ~~~~

Compruebe que los paquetes se han instalado.
   ~~~~
   installed.packages()
   ~~~~



## <a name="acknowledgements"></a>Confirmaciones

El origen de esta información es este artículo de Andre de Vries, quien también ha desarrollado el paquete de miniCRAN. Para obtener más información y un tutorial completo, consulte [How to install R packages on an off-line SQL Server 2016 instance](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) (Cómo instalar paquetes de R en una instancia de SQL Server 2016 sin conexión).

