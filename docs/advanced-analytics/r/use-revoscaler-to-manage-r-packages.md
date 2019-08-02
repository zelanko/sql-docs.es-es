---
title: Cómo usar las funciones de RevoScaleR para buscar o instalar paquetes de R
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8db20295c2e21b6499d4d935f9c99161983b588f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715582"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>Cómo usar las funciones de RevoScaleR para buscar o instalar paquetes de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR 9.0.1 y versiones posteriores incluyen funciones para la administración de paquetes de R en un contexto de proceso de SQL Server. Estas funciones las pueden usar los usuarios remotos y no administradores para instalar paquetes en SQL Server sin acceso directo al servidor.

SQL Server Machine Learning Services ya incluye una versión más reciente de RevoScaleR. Los clientes de SQL Server 2016 R Services deben realizar una [actualización de componentes](../install/upgrade-r-and-python.md) para obtener las funciones de administración de paquetes de RevoScaleR. Para obtener instrucciones sobre cómo recuperar la versión del paquete y el contenido, consulte [obtener información del paquete](../package-management/installed-package-information.md).

## <a name="revoscaler-functions-for-package-management"></a>Funciones de RevoScaleR para la administración de paquetes

En la tabla siguiente se describen las funciones que se usan para la instalación y administración de paquetes de R.

| Función | Descripción |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | Determine la ruta de acceso de la biblioteca de instancias en el SQL Server remoto. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | Obtiene la ruta de acceso de uno o varios paquetes en el SQL Server remoto. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | Llame a esta función desde un cliente remoto de R para instalar paquetes en un contexto de proceso de SQL Server, ya sea desde un repositorio especificado o leyendo paquetes comprimidos guardados localmente. Esta función comprueba las dependencias y garantiza que los paquetes relacionados se puedan instalar en SQL Server, al igual que la instalación del paquete de R en el contexto de proceso local. Para usar esta opción, debe tener habilitada la administración de paquetes en el servidor y en la base de datos. Los entornos de cliente y servidor deben tener la misma versión de RevoScaleR. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | Obtiene una lista de los paquetes instalados en el contexto de proceso especificado. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | Copiar información acerca de una biblioteca de paquetes entre el sistema de archivos y la base de datos para el contexto de proceso especificado. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | Quita los paquetes de un contexto de proceso especificado. También calcula las dependencias y garantiza que se quiten los paquetes que ya no usan otros paquetes en SQL Server, para liberar recursos. |

## <a name="prerequisites"></a>Requisitos previos

+ [Habilitar la administración remota de paquetes de R en SQL Server](r-package-how-to-enable-or-disable.md)

+ Las versiones de RevoScaleR deben ser las mismas en los entornos de cliente y servidor. Para obtener más información, vea [obtener información de paquetes](../package-management/installed-package-information.md).

+ Permiso para conectarse al servidor y a una base de datos, y para ejecutar comandos de R. Debe ser miembro de un rol de base de datos que le permita instalar paquetes en la instancia y la base de datos especificadas.

+ Los usuarios que pertenecen al rol en una base de datos especificada `rpkgs-shared` pueden instalar paquetes en el **ámbito compartido** . Todos los usuarios de este rol pueden desinstalar paquetes compartidos.

+ Cualquier usuario que pertenezca al rol en una base de datos puede instalar `rpkgs-private` los paquetes en el **ámbito privado** . Sin embargo, los usuarios solo pueden ver y desinstalar sus propios paquetes.

+ Los propietarios de bases de datos pueden trabajar con paquetes compartidos o privados.

## <a name="client-connections"></a>Conexiones de cliente

Una estación de trabajo cliente se puede [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) o un [Microsoft machine learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (los científicos de datos suelen usar la edición gratuita para desarrolladores) en la misma red.

Al llamar a funciones de administración de paquetes desde un cliente remoto de R, debe crear primero un objeto de contexto de cálculo mediante la función [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) . A partir de ese momento, para cada función de administración de paquetes que use, pase el contexto de cálculo como argumento.

La identidad del usuario se especifica normalmente al establecer el contexto de cálculo. Si no especifica un nombre de usuario y una contraseña al crear el contexto de cálculo, se usa la identidad del usuario que ejecuta el código de R.

1. En una línea de comandos de R, defina una cadena de conexión para la instancia de y la base de datos de.
2. Use el constructor [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) para definir un contexto de cálculo de SQL Server, mediante la cadena de conexión.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Cree una lista de los paquetes que desea instalar y guarde la lista en una variable de cadena.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Llame a [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) y pase el contexto de cálculo y la variable de cadena que contiene los nombres de paquete.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Si se requieren paquetes dependientes, también se instalan, suponiendo que haya una conexión a Internet disponible en el cliente.
    
    Los paquetes se instalan con las credenciales del usuario que realiza la conexión, en el ámbito predeterminado para ese usuario.

## <a name="call-package-management-functions-in-stored-procedures"></a>Llamar a funciones de administración de paquetes en procedimientos almacenados

La leva ejecuta funciones de administración de `sp_execute_external_script`paquetes dentro de. Al hacerlo, la función se ejecuta utilizando el contexto de seguridad del llamador del procedimiento almacenado.

## <a name="examples"></a>Ejemplos

En esta sección se proporcionan ejemplos de cómo usar estas funciones desde un cliente remoto al conectarse a una instancia de SQL Server o a una base de datos como el contexto de cálculo.

En todos los ejemplos, debe proporcionar una cadena de conexión o un contexto de cálculo, que requiere una cadena de conexión. En este ejemplo se proporciona una manera de crear un contexto de cálculo para SQL Server:

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

Dependiendo de dónde se encuentre el servidor y del modelo de seguridad, es posible que deba proporcionar una especificación de dominio y subred en la cadena de conexión, o bien usar un inicio de sesión de SQL. Por ejemplo:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Obtener la ruta de acceso del paquete en un contexto de proceso de SQL Server remoto

En este ejemplo se obtiene la ruta de acceso del paquete **RevoScaleR** en el contexto `sqlcc`de cálculo,.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Resultado**

"C:/archivos de programa/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/Library/RevoScaleR "

> [!TIP]
> Si ha habilitado la opción para ver la salida de la consola SQL, puede obtener mensajes de estado de la función que `print` precede a la instrucción. Una vez que haya terminado de probar el código `consoleOutput` , establezca en false en el constructor de contexto de proceso para eliminar los mensajes.

### <a name="get-locations-for-multiple-packages"></a>Obtener la ubicación de varios paquetes

En el ejemplo siguiente se obtienen las rutas de acceso de los paquetes **RevoScaleR** y **Lattice** , en el `sqlcc`contexto de cálculo,. Para obtener información sobre varios paquetes, pase un vector de cadena que contenga los nombres de paquete.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obtener versiones de paquete en un contexto de cálculo remoto

Ejecute este comando desde una consola de R para obtener el número de compilación y los números de versión de los paquetes instalados en el contexto de proceso, *sqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Resultado**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Instalar un paquete en SQL Server

En este ejemplo se instala el paquete de **previsión** y sus dependencias en el contexto de cálculo.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Quitar un paquete de SQL Server

En este ejemplo se quita el paquete de **previsión** y sus dependencias del contexto de proceso.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>Sincronizar paquetes entre la base de datos y el sistema de archivos

En el ejemplo siguiente se comprueba la base de datos **TestDB**y se determina si todos los paquetes están instalados en el sistema de archivos. Si faltan algunos paquetes, se instalan en el sistema de archivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

La sincronización de paquetes funciona en cada base de datos y por usuario. Para obtener más información, vea [sincronización de paquetes de R para SQL Server](../r/package-install-uninstall-and-sync.md).

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Usar un procedimiento almacenado para enumerar paquetes en SQL Server

Ejecute este comando desde Management Studio u otra herramienta que admita T-SQL para obtener una lista de los paquetes instalados en la instancia actual, usando `rxInstalledPackages` en un procedimiento almacenado.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

La `rxSqlLibPaths` función se puede utilizar para determinar la biblioteca activa usada por SQL Server Machine Learning Services. Este script solo puede devolver la ruta de acceso de la biblioteca del servidor actual. 

```sql
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
+ [Paquetes predeterminados](../package-management/default-packages.md)