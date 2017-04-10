---
title: "Crear un miniCRAN repositorio de paquete Local mediante | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 4
---
# Crear un miniCRAN repositorio de paquete Local mediante
Este tema describe cómo puede crear un repositorio local del paquete de R con el paquete de R **miniCRAN**. 

Porque [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancias normalmente se encuentran en un servidor que no tiene conectividad a Internet, el método estándar de instalación de paquetes de R (el comando R `install.packages()`) puede que no funcione, el instalador del paquete no puede tener acceso a CRAN u otros sitios de réplica.

Hay dos opciones para instalar paquetes desde un recurso compartido local o en el repositorio:

+ Utilice el paquete de miniCRAN para crear un repositorio local de los paquetes que necesita, entonces se instala desde este repositorio. Este tema describe el método miniCRAN.

+ Descargue los paquetes que necesita y sus dependencias, como archivos zip y guardarlos en una carpeta local y, a continuación, copie esa carpeta a la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo. Para obtener más información sobre el método de copia manual, consulte [instalar paquetes adicionales de SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).


## Paso 1. Instalar miniCRAN y descargue los paquetes 


1. Instale el paquete de miniCRAN en un equipo que tenga acceso a Internet.

   ~~~~
   # Install miniCRAN ---------------------------------------------------

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. Descargar o instalar los paquetes que necesita para este equipo. Esto creará la estructura de carpetas que necesita para copiar los paquetes a la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] más adelante.

   ~~~~
   # List the packages you need 
   # Do not specify dependencies
   pkgs_needed <- c("ggplot2", "ggdendro")
   ~~~~

3. Copiar el repositorio miniCRAN a la biblioteca R_SERVICES la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia.

## Paso 2. Instale los paquetes en el equipo de SQL Server 

4. En la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo, ejecute el comando R  `install.packages()`. Puede utilizar una de las herramientas de R que se instalan con [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], como Rgui.exe, o bien puede ejecutar el comando como parte de una [!INCLUDE[tsql_md](../../includes/tsql-md.md)] procedimiento almacenado.
5. En el símbolo del sistema para especificar un repositorio, seleccione la carpeta que contiene los archivos que acaba de copiar; es decir, el repositorio local miniCRAN.

   ~~~~
   pkgs_needed <- c("ggplot2", "ggdendro")
   local_repo  <- "~/miniCRAN"
   
   .libPaths()[1]
   "C:/Program Files/Microsoft SQL Server/130/R_SERVER/library"

   lib <- .libPaths()[1]

   install.packages(pkgs_needed, 
                 repos = file.path("file://", normalizePath(local_repo, winslash = "/")),
                 lib = lib,
                 type = "win.binary",
                 dependencies = TRUE
                 )
   ~~~~

6. Compruebe que los paquetes se han instalado mediante la ejecución de este código R.
   ~~~~
   installed.packages()
   ~~~~



## Confirmaciones

El origen de esta información es en este artículo, Andre de Vries, que también desarrolló el paquete miniCRAN. Para obtener más información y un tutorial completo, vea  [cómo instalar R paquetes en una instancia de SQL Server 2016 fuera de línea](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)