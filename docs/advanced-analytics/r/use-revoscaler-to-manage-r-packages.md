---
title: "Cómo utilizar las funciones de RevoScaleR para buscar o instalar R paquetes en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 6b8b3e3f50483d51b5e8f7533055d982b6bc6ab3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Cómo utilizar las funciones de RevoScaleR para buscar o instalar paquetes de R en SQL Server

Versión de Microsoft R Server 9.0.1 introdujo nuevas funciones de RevoScaleR que permiten trabajar con paquetes instalados en un contexto de proceso de SQL Server. Estas nuevas funciones facilitan científico de datos ejecutar código R en SQL Server sin acceso directo al servidor.

Cada científico de datos puede instalar paquetes privados que no son visibles para otros usuarios. Dado que los paquetes se pueden alcanzar a una base de datos y cada usuario obtenga un espacio aislado de paquete aislado en cada base de datos, es más fácil instalar diferentes versiones del mismo paquete de R.

Si migra la base de datos de trabajo a un nuevo servidor, también puede utilizar la función de sincronización de paquete para leer una lista de todos los paquetes e instalarlos en una base de datos en el nuevo servidor.

En este artículo se describe estas funciones y se proporciona ejemplos de uso de las funciones.

## <a name="requirements"></a>Requisitos

+ Para ejecutar estas funciones, debe tener permiso para ejecutar comandos de R en la instancia.

+ Si no especifica un nombre de usuario y una contraseña cuando se crea el contexto de proceso, se utiliza la identidad del usuario que ejecuta el código de R.

+ Cuando se utilizan estas funciones desde un cliente remoto de R, debe crear un objeto de contexto de proceso en primer lugar, mediante la función RxInSQLServer. Por lo tanto, para cada función de administración de paquetes que usa, pase el contexto de proceso como argumento.

+ Es posible ejecutar funciones de administración de paquetes mediante `sp_execute_external_script`. Al hacerlo, la función se ejecuta utilizando el contexto de seguridad del autor de la llamada de procedimiento almacenado.

## <a name="list-of-package-management-functions"></a>Lista de funciones de administración de paquetes

Se proporcionan las siguientes funciones de administración de paquetes en RevoScaleR, para la instalación y eliminación de paquetes en un contexto de proceso especificado:

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): buscar información acerca de los paquetes instalados en el contexto de proceso especificado.

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): instalar paquetes en un contexto de proceso, ya sea desde un repositorio especificado o leyendo guardados localmente zip paquetes.

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): quitar los paquetes instalados en un contexto de proceso.

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): obtener la ruta de acceso para uno o varios paquetes en el contexto de proceso especificado.

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): copia de una biblioteca de paquetes entre el sistema de archivos y bases de datos en los contextos de proceso especificado.

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): obtener la ruta de acceso de búsqueda para los árboles de biblioteca para los paquetes mientras se ejecuta dentro de SQL Server.

Estos paquetes se incluyen de forma predeterminada en SQL Server 2017. Para obtener información acerca de estas funciones, vea las páginas de referencia de la función de RevoScaleR: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

> [!NOTE]
> Funciones de R para administración de paquetes son disponible a partir Microsoft R Server 9.0.1. Si no encuentra las funciones de RevoScaleR, probablemente deba actualizar a la versión más reciente. 
## <a name="examples"></a>Ejemplos

Esta sección contiene ejemplos de cómo usar las funciones de administración del paquete con una instancia de SQL Server o la base de datos. 

+ Las funciones de instalación de paquetes comprueban si hay dependencias y se aseguran de que se puedan instalar todos los paquetes relacionados en SQL Server, como la instalación de paquetes de R en el contexto de proceso local.

+ La función que _desinstala_ paquetes también calcula las dependencias y se asegura de que se quitan los paquetes que ya no se utilizan otros paquetes en SQL Server, para liberar recursos.

+ Puede usar una combinación de los usuarios y el ámbito para buscar paquetes o agregar paquetes a una base de datos determinada:

    + Paquetes de **ámbito compartido** puede instalarse con los usuarios que pertenecen a la `rpkgs-shared` rol en una base de datos especificada. Todos los usuarios de este rol pueden desinstalar paquetes compartidos.
    + Paquetes de **ámbito privado** se puede instalar cualquier usuario que pertenezca a la `rpkgs-private` rol en una base de datos. Sin embargo, los usuarios pueden ver y desinstalar sólo sus propios paquetes.
    + Los propietarios de base de datos pueden trabajar con paquetes compartidos o privados.

**Desde el código de R**

Si tiene permiso para instalar paquetes, ejecute una del paquete de funciones de administración desde el cliente de R y especificar el contexto de proceso donde los paquetes son para agregarse o quitarse.  El contexto de proceso puede ser el equipo local o una base de datos de la instancia de SQL Server. Las credenciales de determinan si se puede completar la operación en el servidor.

**De Transact-SQL**

Para ejecutar las funciones de administración del paquete desde un procedimiento almacenado, agruparlos en una llamada a `sp_execute_external_script`.

### <a name="get-list-of-packages-in-a-sql-server-compute-context"></a>Obtener lista de paquetes en un contexto de proceso de SQL Server

Este ejemplo se comprueba para los paquetes que se instalaron en la instancia `myServer`, en la base de datos `TestDB`. Administración de paquetes se limita a una base de datos específica y el usuario. Si el usuario no se especifica, se supone que el usuario que ejecuta la llamada de contexto de proceso. Para obtener más información, consulte [Scoping de paquetes por rol](#bkmk_scope).

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obtener la ruta de acceso de paquete en un contexto de proceso de SQL Server remoto

En este ejemplo se obtiene la ruta de acceso del paquete **RevoScaleR** en el contexto del proceso, *sqlServer*.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>Obtener la ubicación de varios paquetes

En el ejemplo siguiente se obtienen las rutas de acceso de los paquetes **RevoScaleR** y **lattice** en el contexto de proceso, *sqlServer*. Para obtener información acerca de varios paquetes, pase un vector de cadena que contiene los nombres de paquete.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```


### <a name="get-package-versions-on-a-remote-compute-context"></a>Obtener las versiones del paquete en un contexto de proceso remoto.

Ejecute este comando desde una consola de R para obtener el número de compilación y los números de versión para los paquetes instalados en el contexto de proceso, *sqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Instalar un paquete en SQL Server

Este ejemplo se instala la **previsión** paquete y sus dependencias en el contexto de proceso, *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>Quitar un paquete de SQL Server

En este ejemplo se quita el paquete **ggplot2** y sus dependencias del contexto de proceso, *sqlServer*.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>Sincronizar los paquetes entre el sistema de archivos y la base de datos

En el ejemplo siguiente se comprueba la base de datos **TestDB**y determina si todos los paquetes se instalan en el sistema de archivos. Si faltan algunos paquetes, se instalan en el sistema de archivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

Sincronización de paquetes funciona en una cada base de datos y por usuario. Para obtener más información, consulte [sincronización de paquetes de R para SQL Server](../r/package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Usar un procedimiento almacenado para enumerar los paquetes en SQL Server

Ejecute este comando desde Management Studio u otra herramienta que admita T-SQL, para obtener una lista de los paquetes instalados en la instancia actual, mediante `rxInstalledPackages` en un procedimiento almacenado.

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

El `rxSqlLibPaths` función puede utilizarse para determinar la biblioteca active utilizada por servicios de aprendizaje de máquina de SQL Server. Esta secuencia de comandos puede devolver la ruta de biblioteca para el servidor actual. 

```SQL
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```
