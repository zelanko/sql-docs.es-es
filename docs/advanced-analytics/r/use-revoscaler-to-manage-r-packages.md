---
title: Cómo utilizar las funciones de RevoScaleR para buscar o instalar R paquetes en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d92b3e993968ce48d7489b0c17d6bdba005809a3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707533"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Cómo utilizar las funciones de RevoScaleR para buscar o instalar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 y versiones posteriores se incluyen funciones de administración de paquetes de R en un contexto de proceso de SQL Server. Estas funciones se pueden usar remoto, que no sean administradores para instalar paquetes en SQL Server sin acceso directo al servidor.

Servicios de aprendizaje de SQL Server de 2017 máquina ya incluye una versión más reciente de RevoScaleR. Los clientes de SQL Server 2016 R Services deben dedicar un [actualización del componente](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) obtener funciones de administración del paquete RevoScaleR. Para obtener instrucciones sobre cómo recuperar paquete de versión y el contenido, consulte [obtener información de paquete](determine-which-packages-are-installed-on-sql-server.md).

## <a name="revoscaler-functions-for-package-management"></a>Funciones de RevoScaleR para administración de paquetes

En la tabla siguiente se describe las funciones usadas para la administración e instalación de paquete de R.

| Función | Descripción |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determinar la ruta de acceso de la biblioteca de la instancia en el servidor SQL remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Obtiene la ruta de acceso para uno o varios paquetes en el servidor SQL remoto. |
| [rxInstallPackages](https://docs.microsoft.com/en-us/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Llame a esta función desde un cliente remoto de R para instalar paquetes en un contexto de proceso de SQL Server, ya sea desde un repositorio especificado o leyendo guardados localmente paquetes comprimidos. Esta función comprueba las dependencias y se asegura de que se pueden instalar todos los paquetes relacionados con SQL Server, igual que la instalación del paquete de R en el contexto de proceso local. Para usar esta opción, debe haber habilitado la administración de paquetes en el servidor y la base de datos. Entornos de cliente y el servidor deben tener la misma versión de RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Obtiene una lista de paquetes instalados en el contexto de proceso especificado. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copiar información sobre una biblioteca de paquetes entre el sistema de archivos y la base de datos, el contexto de proceso especificado. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Quita los paquetes de un contexto de proceso especificado. También calcula las dependencias y se asegura de que se quitan los paquetes que ya no se utilizan otros paquetes en SQL Server, para liberar recursos. |

## <a name="prerequisites"></a>Requisitos previos

+ [Habilitar la administración remota del paquete de R en SQL Server](r-package-how-to-enable-or-disable.md)

+ Versiones de RevoScaleR deben ser los mismos en entornos de cliente y servidor. Para obtener más información, consulte [obtener información de paquete](determine-which-packages-are-installed-on-sql-server.md).

+ Permiso para conectarse al servidor y una base de datos y ejecutar comandos de R. Debe ser un miembro de un rol de base de datos que le permite instalar paquetes en la instancia especificada y la base de datos.

+ Paquetes de **ámbito compartido** puede instalarse con los usuarios que pertenecen a la `rpkgs-shared` rol en una base de datos especificada. Todos los usuarios de este rol pueden desinstalar paquetes compartidos.

+ Paquetes de **ámbito privado** se puede instalar cualquier usuario que pertenezca a la `rpkgs-private` rol en una base de datos. Sin embargo, los usuarios pueden ver y desinstalar sólo sus propios paquetes.

+ Los propietarios de base de datos pueden trabajar con paquetes compartidos o privados.

## <a name="client-connections"></a>Conexiones de cliente

Puede ser una estación de trabajo cliente [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) o un [aprendizaje de máquina de Microsoft Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (los científicos de datos suelen utilizar la edición de desarrollador gratuita) en la misma red.

Al llamar a funciones de administración del paquete desde un cliente remoto de R, debe crear un objeto de contexto de proceso en primer lugar, mediante el [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) (función). Por lo tanto, para cada función de administración de paquetes que usa, pase el contexto de proceso como argumento.

Normalmente, se especifica la identidad del usuario al establecer el contexto de proceso. Si no especifica un nombre de usuario y una contraseña cuando se crea el contexto de proceso, se utiliza la identidad del usuario que ejecuta el código de R.

1. Desde una línea de comandos de R, definir una cadena de conexión a la instancia y la base de datos.
2. Use la [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) constructor para definir un contexto de proceso de SQL Server, utilizando la cadena de conexión.

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

    Si se requieren paquetes dependientes, también se instalan, suponiendo que una conexión a internet está disponible en el cliente.
    
    Los paquetes se instalan con las credenciales del usuario que realiza la conexión, en el ámbito predeterminado para ese usuario.

## <a name="call-package-management-functions-in-stored-procedures"></a>Llamar a funciones de administración de paquetes en los procedimientos almacenados

Cámara ejecutar funciones de administración de paquetes dentro de `sp_execute_external_script`. Al hacerlo, la función se ejecuta utilizando el contexto de seguridad del autor de la llamada de procedimiento almacenado.

## <a name="examples"></a>Ejemplos

Esta sección proporciona ejemplos de cómo usar estas funciones desde un cliente remoto cuando se conecta a una instancia de SQL Server o la base de datos como el contexto de proceso.

Para obtener todos los ejemplos, debe proporcionar una cadena de conexión o un contexto de proceso, lo que requiere una cadena de conexión. Este ejemplo proporciona una manera de crear un contexto de proceso para SQL Server:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

Dependiendo de dónde se encuentra el servidor y el modelo de seguridad, deberá proporcionar una especificación de dominio y la subred en la cadena de conexión, o usar un inicio de sesión SQL. Por ejemplo:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obtener la ruta de acceso de paquete en un contexto de proceso de SQL Server remoto

Este ejemplo obtiene la ruta de acceso para la **RevoScaleR** paquete en el contexto de proceso, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Resultado**

"C:/programa archivos/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> Si ha habilitado la opción Ver la salida de la consola SQL, podría obtener mensajes de estado de la función que precede a la `print` instrucción. Cuando haya terminado de probar el código, establezca `consoleOutput` en FALSE en el constructor de contexto de proceso para eliminar los mensajes.

### <a name="get-locations-for-multiple-packages"></a>Obtener la ubicación de varios paquetes

El ejemplo siguiente obtiene las rutas de acceso para la **RevoScaleR** y **celosía** paquetes, en el contexto de proceso, `sqlcc`. Para obtener información acerca de varios paquetes, pase un vector de cadena que contiene los nombres de paquete.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obtener las versiones del paquete en un contexto de proceso remoto.

Ejecute este comando desde una consola de R para obtener el número de compilación y los números de versión para los paquetes instalados en el contexto de proceso, *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Resultado**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Instalar un paquete en SQL Server

Este ejemplo se instala la **previsión** paquete y sus dependencias en el contexto de proceso.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Quitar un paquete de SQL Server

Este ejemplo quita la **previsión** paquete y sus dependencias en el contexto de proceso.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
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

## <a name="see-also"></a>Vea también

+ [Habilitación de la administración de paquetes de R remota](r-package-how-to-enable-or-disable.md)
+ [Sincronización de paquetes de R](package-install-uninstall-and-sync.md)
+ [Sugerencias para la instalación de paquetes de R](packages-installed-in-user-libraries.md)
+ [Paquetes predeterminados](installing-and-managing-r-packages.md)