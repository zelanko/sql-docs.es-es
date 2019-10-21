---
title: Instalar nuevos paquetes de R con sqlmlutils
description: Aprenda a usar sqlmlutils para instalar nuevos paquetes de R en una instancia de SQL Server Machine Learning Services o SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f8ce5c7bcf12a2431c2de779912d2e309c628cb1
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542144"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Instalar nuevos paquetes de R con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo usar las funciones del paquete [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar nuevos paquetes de R en una instancia de SQL Server Machine Learning Services o SQL Server R Services. Los paquetes que se instalan se pueden usar en scripts de R que se ejecutan en la base de datos mediante la instrucción T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) .

> [!NOTE]
> No se recomienda el comando estándar de R `install.packages` para agregar paquetes de R en SQL Server. En su lugar, use **sqlmlutils** como se describe en este artículo.

## <a name="prerequisites"></a>Prerequisites

- Instale [R](https://www.r-project.org) y [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) en el equipo cliente que usa para conectarse a SQL Server. Puede usar cualquier IDE de R para ejecutar scripts, pero en este artículo se da por supuesto que RStudio.

- Instale [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) en el equipo cliente que usa para conectarse a SQL Server. Puede usar otras herramientas de consulta o administración de bases de datos, pero en este artículo se da por supuesto Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Otras consideraciones

- El script de R que se ejecuta en SQL Server solo puede usar los paquetes instalados en la biblioteca de instancia predeterminada. SQL Server no puede cargar paquetes de bibliotecas externas, aunque la biblioteca esté en el mismo equipo. Esto incluye las bibliotecas de R instaladas con otros productos de Microsoft.

- En un entorno de SQL Server protegido, puede que desee evitar lo siguiente:
  - Paquetes que requieren acceso a la red
  - Paquetes que requieren acceso al sistema de archivos elevado
  - Paquetes usados para el desarrollo web u otras tareas que no se benefician al ejecutarse dentro de SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalación de sqlmlutils en el equipo cliente

Para usar **sqlmlutils**, primero debe instalarlo en el equipo cliente que usa para conectarse a SQL Server.

El paquete **sqlmlutils** depende del paquete **RODBCext** y **RODBCext** depende de varios otros paquetes. En los procedimientos siguientes se instalan todos estos paquetes en el orden correcto.

### <a name="install-sqlmlutils-online"></a>Instalación de sqlmlutils online

Si el equipo cliente tiene acceso a Internet, puede descargar e instalar **sqlmlutils** y sus paquetes dependientes en línea.

1. Descargue el archivo zip de **sqlmlutils** más reciente de https://github.com/Microsoft/sqlmlutils/tree/master/R/dist en el equipo cliente. No descomprima el archivo.

1. Abra un **símbolo del sistema** y ejecute los siguientes comandos para instalar los paquetes **sqlmlutils** y **RODBCext**. Reemplace la ruta de acceso completa al archivo zip de **sqlmlutils** que ha descargado (en este ejemplo se da por supuesto que el archivo está en la carpeta de documentos). El paquete **RODBCext** se encuentra en línea e instalado.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Instalación de sqlmlutils sin conexión

Si el equipo cliente no tiene una conexión a Internet, debe descargar los paquetes **sqlmlutils** y **RODBCext** de antemano con un equipo que tenga acceso a Internet. Después, puede copiar los archivos en una carpeta en el equipo cliente e instalar los paquetes sin conexión.

El paquete **RODBCext** tiene varios paquetes dependientes y la identificación de todas las dependencias de un paquete resulta complicada. Se recomienda usar [**miniCRAN**](https://andrie.github.io/miniCRAN/) para crear una carpeta de repositorio local para el paquete que incluya todos los paquetes dependientes.
Para obtener más información, vea [crear un repositorio de paquetes de R local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

El paquete **sqlmlutils** consta de un solo archivo zip que se puede copiar en el equipo cliente e instalar.

En un equipo con acceso a Internet:

1. Instale **miniCRAN**. Consulte [instalación de miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obtener más información.

1. En RStudio, ejecute el siguiente script de R para crear un repositorio local del paquete **RODBCext**. En este ejemplo se crea el repositorio en la carpeta `c:\downloads\rodbcext`.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end

   Para el valor `Rversion`, use la versión de R instalada en SQL Server. Para comprobar la versión instalada, use el siguiente comando de T-SQL.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Descargue el archivo zip de **sqlmlutils** más reciente de https://github.com/Microsoft/sqlmlutils/tree/master/R/dist (no descomprima el archivo). Por ejemplo, descargue el archivo en `c:\downloads\sqlmlutils_0.7.1.zip`.

1. Copie la carpeta del repositorio **RODBCext** completa (`c:\downloads\rodbcext`) y el archivo zip **sqlmlutils** (`c:\downloads\sqlmlutils_0.7.1.zip`) en el equipo cliente. Por ejemplo, cópielos en la carpeta `c:\temp\packages` en el equipo cliente.

En el equipo cliente que usa para conectarse a SQL Server, abra un símbolo del sistema y ejecute los siguientes comandos para instalar **RODBCext** y, a continuación, **sqlmlutils**.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>Agregar un paquete de R en SQL Server

En el ejemplo siguiente, agregará el paquete [**glue**](https://cran.r-project.org/web/packages/glue/) a SQL Server.

### <a name="add-the-package-online"></a>Agregar el paquete en línea

Si el equipo cliente que usa para conectarse a SQL Server tiene acceso a Internet, puede usar **sqlmlutils** para buscar el paquete de **adherencia** y las dependencias a través de Internet y, a continuación, instalar el paquete en una instancia de SQL Server de forma remota.

1. En el equipo cliente, abra RStudio y cree un nuevo archivo de **script de R** .

1. Use el siguiente script de R para instalar el paquete de **glue** mediante **sqlmlutils**. Sustituya su propia información de conexión de base de datos SQL Server (si no utiliza la autenticación de Windows, agregue `uid` y `pwd` parámetros).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > El **ámbito** puede ser **público** o **privado**. El ámbito público es útil para que el administrador de bases de datos Instale paquetes que todos los usuarios pueden usar. Ámbito privado hace que el paquete esté disponible solo para el usuario que lo instala. Si no especifica el ámbito, el ámbito predeterminado es **privado**.

### <a name="add-the-package-offline"></a>Agregar el paquete sin conexión

Si el equipo cliente no tiene una conexión a Internet, puede usar **miniCRAN** para descargar el paquete de **glue** mediante un equipo que tenga acceso a Internet. A continuación, copie el paquete en el equipo cliente en el que puede instalar el paquete sin conexión.
Consulte [instalación de miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obtener información sobre la instalación de **miniCRAN**.

En un equipo con acceso a Internet:

1. Ejecute el siguiente script de R para crear un repositorio local para el **pegado**. En este ejemplo se crea la carpeta del repositorio en `c:\downloads\glue`.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.microsoft.com")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end


   Para el valor `Rversion`, use la versión de R instalada en SQL Server. Para comprobar la versión instalada, use el siguiente comando de T-SQL.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. Copie toda la carpeta del repositorio de **adherencia** (`c:\downloads\glue`) en el equipo cliente. Por ejemplo, cópielo en la carpeta `c:\temp\packages\glue`.

En el equipo cliente:

1. Abra RStudio y cree un nuevo archivo de **script de R** .

1. Use el siguiente script de R para instalar el paquete de **glue** mediante **sqlmlutils**. Sustituya su propia información de conexión de base de datos SQL Server (si no utiliza la autenticación de Windows, agregue `uid` y `pwd` parámetros).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > El **ámbito** puede ser **público** o **privado**. El ámbito público es útil para que el administrador de bases de datos Instale paquetes que todos los usuarios pueden usar. Ámbito privado hace que el paquete esté disponible solo para el usuario que lo instala. Si no especifica el ámbito, el ámbito predeterminado es **privado**.

## <a name="use-the-package"></a>Usar el paquete

Una vez instalado el paquete de **adherencia** , puede usarlo en un script de R en SQL Server con el comando **sp_execute_external_script** de T-SQL.

1. Abra Azure Data Studio o SSMS y conéctese a la base de datos de SQL Server.

1. Ejecute el siguiente comando:

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **Resultado**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>Quitar el paquete

Si desea quitar el paquete de **adherencia** , ejecute el siguiente script de R. Use la misma variable de **conexión** que definió anteriormente.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre los paquetes de R instalados, vea [obtener información de paquetes de r](r-package-information.md) .
- Para obtener ayuda para trabajar con paquetes de R, consulte [sugerencias para usar paquetes de r](tips-for-using-r-packages.md) .
- Para obtener información sobre la instalación de paquetes de Python, consulte [instalación de paquetes de Python con PIP](install-additional-python-packages-on-sql-server.md) .
- Para obtener más información acerca de SQL Server Machine Learning Services, consulte [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
