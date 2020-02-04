---
title: Instalación de paquetes de R adicionales
description: Aprenda a usar sqlmlutils para instalar nuevos paquetes de R en una instancia de SQL Server Machine Learning Services o SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/20/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e9435c52cc0bf318291d38a2511f496c818c2fd6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "74479432"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Instalación de nuevos paquetes de R con sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe cómo usar las funciones del paquete de [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar nuevos paquetes de R en una instancia de SQL Server Machine Learning Services o SQL Server R Services. Los paquetes que se instalen podrán usarse en los scripts de R que se ejecutan en la base de datos mediante la instrucción T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

> [!NOTE]
> No se recomienda usar el comando estándar de R `install.packages` para agregar paquetes de R en SQL Server. Use en su lugar **sqlmlutils**, como se describe en este artículo.

## <a name="prerequisites"></a>Prerequisites

- Instale [R](https://www.r-project.org) y [RStudio Desktop](https://www.rstudio.com/products/rstudio/download/) en el equipo cliente que usa para conectarse a SQL Server. Puede usar cualquier IDE de R para ejecutar scripts, pero en este artículo se da por supuesto que es RStudio.

- Instale [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) en el equipo cliente que usa para conectarse a SQL Server. Puede usar otras herramientas de consulta o administración de bases de datos, pero en este artículo se da por supuesto que emplea Azure Data Studio o SSMS.

### <a name="other-considerations"></a>Otras consideraciones

- El script de R que se ejecuta en SQL Server solo puede usar los paquetes instalados en la biblioteca de instancia predeterminada. SQL Server no puede cargar paquetes de bibliotecas externas, aunque la biblioteca esté en el mismo equipo. Esto incluye las bibliotecas de R instaladas con otros productos de Microsoft.

- En un entorno de SQL Server protegido, probablemente le interese evitar lo siguiente:
  - Paquetes que requieren acceso a la red
  - Paquetes que requieren acceso con privilegios elevados al sistema de archivos
  - Paquetes que se usan para el desarrollo web u otras tareas que no obtienen ningún beneficio al ejecutarse en SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalación de sqlmlutils en el equipo cliente

Para usar **sqlmlutils**, primero debe instalarlo en el equipo cliente que usa para conectarse a SQL Server.

El paquete de **sqlmlutils** depende del paquete de **RODBCext** y **RODBCext** depende de otros paquetes. En los procedimientos siguientes se instalan todos estos paquetes en el orden correcto.

### <a name="install-sqlmlutils-online"></a>Instalación de sqlmlutils en línea

Si el equipo cliente tiene acceso a Internet, puede descargar e instalar **sqlmlutils** y sus paquetes dependientes en línea.

1. Descargue el archivo .zip **sqlmlutils** más reciente desde https://github.com/Microsoft/sqlmlutils/tree/master/R/dist en el equipo cliente. No descomprima el archivo.

1. Abra un **símbolo del sistema** y ejecute el comando siguiente para instalar los paquetes **sqlmlutils** y **RODBCext**. Sustituya la ruta de acceso completa del archivo ZIP **sqlmlutils** que ha descargado (en este ejemplo, se da por supuesto que el archivo descargado se encuentra en la carpeta Documentos). El paquete de **RODBCext** se encuentra en línea y está instalado.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Instalación de sqlmlutils sin conexión

Si el equipo cliente no tiene una conexión a Internet, debe descargar los paquetes **sqlmlutils** y **RODBCext** con antelación mediante un equipo que no tenga acceso a Internet. Después, puede copiar los archivos en una carpeta en el equipo cliente e instalar los paquetes sin conexión.

El paquete de **RODBCext** tiene varios paquetes dependientes, y resulta complicado identificar todas las dependencias de un paquete. Recomendamos usar [**miniCRAN**](https://andrie.github.io/miniCRAN/) para crear una carpeta de repositorio local para el paquete que incluya todos los paquetes dependientes.
Para obtener más información, consulte [Creación de un repositorio de paquete de R local mediante miniCRAN](create-a-local-package-repository-using-minicran.md).

El paquete de **sqlmlutils** consta de un solo archivo zip que se puede copiar e instalar en el equipo cliente.

En un equipo con acceso a Internet:

1. Instale **miniCRAN**. Para obtener más información, consulte [Instalación de miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran).

1. En RStudio, ejecute el siguiente script de R para crear un repositorio local del paquete **RODBCext**. En este ejemplo, se crea el repositorio en la carpeta `c:\downloads\rodbcext`.

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

1. Descargue el archivo ZIP **sqlmlutils** más reciente desde https://github.com/Microsoft/sqlmlutils/tree/master/R/dist (no descomprima el archivo). Por ejemplo, descargue el archivo en `c:\downloads\sqlmlutils_0.7.1.zip`.

1. Copie toda la carpeta del repositorio de **RODBCext** (`c:\downloads\rodbcext`) y el archivo zip de **sqlmlutils** (`c:\downloads\sqlmlutils_0.7.1.zip`) en el equipo cliente. Por ejemplo, cópielos en la carpeta `c:\temp\packages` en el equipo cliente.

En el equipo cliente que usa para conectarse a SQL Server, abra un símbolo del sistema y ejecute los comandos siguientes para instalar **RODBCext** y, a continuación, **sqlmlutils**.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>Adición de un paquete de R en SQL Server

En el ejemplo siguiente, agregará el paquete de [**glue**](https://cran.r-project.org/web/packages/glue/) a SQL Server.

### <a name="add-the-package-online"></a>Adición del paquete en línea

Si el equipo cliente que usa para conectarse a SQL Server tiene acceso a Internet, puede usar **sqlmlutils** para buscar el paquete de **glue** y las dependencias a través de Internet y, después, instalar el paquete en una instancia de SQL Server de forma remota.

1. En el equipo cliente, abra RStudio y cree un nuevo archivo de **script de R**.

1. Use el siguiente script de R para instalar el paquete de **glue** mediante **sqlmlutils**. Sustituya su propia información de conexión de base de datos de SQL Server (si no usa la autenticación de Windows, agregue los parámetros `uid` y `pwd`).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > El **ámbito** puede ser **PÚBLICO** o **PRIVADO**. El ámbito público es útil para que el administrador de bases de datos instale paquetes que todos los usuarios pueden usar. El ámbito privado hace que el paquete esté disponible solo para el usuario que lo instala. Si no especifica el ámbito, el ámbito predeterminado es **PRIVADO**.

### <a name="add-the-package-offline"></a>Adición del paquete sin conexión

Si el equipo cliente no tiene una conexión a Internet, puede utilizar **miniCRAN** para descargar el paquete de **glue** mediante un equipo que no tenga acceso a Internet. Después, copie el paquete en el equipo cliente en el que puede instalar el paquete sin conexión.
Consulte [Instalación de miniCRAN](create-a-local-package-repository-using-minicran.md#install-minicran) para obtener información sobre cómo instalar **miniCRAN**.

En un equipo con acceso a Internet:

1. Ejecute el siguiente script de R para crear un repositorio local para **glue**. En este ejemplo, la carpeta del repositorio se crea en `c:\downloads\glue`.

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

1. Copie toda la carpeta del repositorio de **glue** (`c:\downloads\glue`) en el equipo cliente. Por ejemplo, cópiela en la carpeta `c:\temp\packages\glue`.

En el equipo cliente:

1. Abra RStudio y cree un nuevo archivo de **script de R**.

1. Use el siguiente script de R para instalar el paquete de **glue** mediante **sqlmlutils**. Sustituya su propia información de conexión de base de datos de SQL Server (si no usa la autenticación de Windows, agregue los parámetros `uid` y `pwd`).

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > El **ámbito** puede ser **PÚBLICO** o **PRIVADO**. El ámbito público es útil para que el administrador de bases de datos instale paquetes que todos los usuarios pueden usar. El ámbito privado hace que el paquete esté disponible solo para el usuario que lo instala. Si no especifica el ámbito, el ámbito predeterminado es **PRIVADO**.

## <a name="use-the-package"></a>Uso del paquete

Una vez instalado el paquete de **glue**, puede usarlo en un script de R en SQL Server con el comando T-SQL **sp_execute_external_script**.

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

    **Resultados**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>Eliminación del paquete

Si desea eliminar el paquete de **glue**, ejecute el siguiente script de R. Use la misma variable de **conexión** que definió anteriormente.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre los paquetes de R instalados, consulte [Obtener información de paquetes de R](r-package-information.md).
- Para obtener ayuda para trabajar con paquetes de R, consulte [Sugerencias para usar paquetes de R](tips-for-using-r-packages.md).
- Para obtener información sobre la instalación de paquetes de Python, consulte [Instalación de paquetes de Python con PIP](install-additional-python-packages-on-sql-server.md).
- Para obtener más información sobre SQL Server Machine Learning Services, consulte [¿Qué es SQL Server Machine Learning Services (Python y R)?](../what-is-sql-server-machine-learning.md)
