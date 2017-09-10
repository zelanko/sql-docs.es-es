---
title: "Administración de paquetes de R para SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f19982251b629d12215595685c0633b4c6b61c98
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="r-package-management-for-sql-server"></a>Administración de paquetes de R para SQL Server

En este tema se describe las características de administración de paquetes que puede usar para administrar paquetes de R que se ejecutan en una instancia de SQL Server.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="package-management-using-t-sql"></a>Administración de paquetes mediante T-SQL

Puede continuar con la instalación de paquetes de R como administrador en el equipo, si tiene los privilegios, y si es la única persona que utiliza el servidor para trabajos de aprendizaje de máquina.

Sin embargo, si tiene que compartir paquetes con otros usuarios, o si necesitan varias personas ejecutar trabajos de aprendizaje de máquina en el servidor, es más eficaz para configurar una biblioteca compartida de paquete. SQL Server admite esto a través de roles de base de datos.

El Administrador de base de datos es responsable de establecer los roles y agregar usuarios a los roles. A través de roles, el Administrador de base de datos puede controlar quién tiene permiso para agregar o quitar paquetes de R desde el entorno de SQL Server y puede auditar la instalación del paquete.

### <a name="database-roles-for-package-management"></a>Roles de base de datos para la administración de paquetes

Los siguientes nuevos roles de base de datos admiten la seguridad de la instalación y administración de paquetes de R en SQL Server:

- `rpkgs-users`: Permite a los usuarios utilizar los paquetes compartidos que se instalaron los miembros de los `rpkgs-shared` rol.

- `rpkgs-private`: Proporciona acceso a los paquetes compartidos con los mismos permisos que los `rpkgs-users` rol. Los miembros de este rol también pueden instalar, quitar y usar paquetes de ámbito privado.

-  `rpkgs-shared`: Proporciona los mismos permisos que los `rpkgs-private` rol. Los usuarios que son miembros de este rol también pueden instalar o quitar paquetes compartidos.

- `db_owner`: Tiene los mismos permisos que los `rpkgs-shared` rol. También puede conceder a los usuarios el derecho de instalar o quitar paquetes compartidos y privados.

### <a name="creating-an-external-package-library-using-t-sql"></a>Crear una biblioteca de paquete externo mediante T-SQL

Además, SQL Server 2017 es compatible con la instrucción T-SQL, **crear biblioteca externa**, para admitir la administración de administrador de base de datos de bibliotecas externas. Actualmente se puede utilizar esta instrucción para crear bibliotecas basadas en Windows para R. adicionales soporte técnico está planeada en el futuro para los paquetes de Python y para los paquetes que se escriben para su ejecución en otras plataformas, como Linux.

Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="package-management-using-r"></a>Administración de paquetes con R

El **RevoScaleR** paquete ahora incluye funciones para admitir la instalación y administración de paquetes de R. Estas nuevas funciones, combinadas con roles de base de datos de administración de paquetes, es compatible con estos escenarios:

- Los científicos de datos pueden instalar paquetes de R necesarios en SQL Server sin tener acceso administrativo al equipo de SQL Server.
- Los paquetes se instalan por la base de datos y, cuando se mueve la base de datos, los paquetes se mueven con él.
- Es más fácil compartir paquetes con otros usuarios. Si configura un repositorio de paquetes local, cada científico de datos puede utilizar el repositorio para instalar paquetes a su base de datos.
- El Administrador de base de datos no es necesario obtener información sobre cómo ejecutar comandos de R y no es necesario realizar un seguimiento de las dependencias de paquetes complejo.
- El DBA puede utilizar los roles de base de datos conocidos para controlar qué usuarios de SQL Server se pueden instalar, desinstalar o utilizar los paquetes.

### <a name="r-package-management-functions"></a>Funciones de administración de paquetes de R

Se proporcionan las siguientes funciones de administración de paquetes en RevoScaleR, para la instalación y eliminación de paquetes en un contexto de proceso especificado:

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): buscar información acerca de los paquetes instalados en el contexto de proceso especificado.

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): instalar paquetes en un contexto de proceso, ya sea desde un repositorio especificado o leyendo guardados localmente zip paquetes.

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): quitar los paquetes instalados en un contexto de proceso.

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): obtener la ruta de acceso para uno o varios paquetes en el contexto de proceso especificado.

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): copia de una biblioteca de paquetes entre el sistema de archivos y bases de datos en los contextos de proceso especificado.

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): obtener la ruta de acceso de búsqueda para los árboles de biblioteca para los paquetes mientras se ejecuta dentro de SQL Server.

Estos paquetes también se incluyen de forma predeterminada en SQL Server 2017. Puede agregar los paquetes a una instancia de SQL Server 2016 si actualiza la instancia para utilizar como mínimo Microsoft R 9.0.1. Para obtener más información, consulte [utilizando SqlBindR.exe para actualizar R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Para obtener información acerca de estas funciones, vea las páginas de referencia de la función de RevoScaleR: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

## <a name="how-package-management-works"></a>Cómo funciona la administración de paquetes

Si tiene permiso para instalar paquetes, ejecute una de las funciones de administración de paquetes desde el código de R y especifique el contexto de proceso en el que se deben agregar o quitar los paquetes. El contexto de proceso puede ser el equipo local o una base de datos de la instancia de SQL Server. Si la llamada a la instalación de paquetes se ejecuta en SQL Server, las credenciales determinan si se puede llevar a cabo la operación en el servidor. Las funciones de instalación de paquetes comprueban si hay dependencias y se aseguran de que se puedan instalar todos los paquetes relacionados en SQL Server, como la instalación de paquetes de R en el contexto de proceso local. La función que desinstala los paquetes también calcula las dependencias y se asegura de que se quiten los paquetes que otros paquetes de SQL Server ya no usan, con el objetivo de liberar recursos.

Cada científico de datos puede instalar paquetes privados que no son visibles para otros usuarios, crear un espacio aislado privado paquetes de R. Dado que los paquetes se pueden alcanzar a una base de datos y cada usuario obtenga un espacio aislado de paquete aislado en cada base de datos, es más fácil instalar diferentes versiones del mismo paquete de R.

Si se migra la base de datos de trabajo a un nuevo servidor, puede usar la función de sincronización de paquete para leer una lista de todos los paquetes e instalarlos en una base de datos en el nuevo servidor.

> [!NOTE]
> 
> Las funciones de R para la administración de paquetes se proporcionan a partir de Microsoft R Server 9.0.1. Si no encuentra las funciones de RevoScaleR, probablemente deba actualizar a la versión más reciente.

### <a name="bkmk_scope"></a>Ámbito de paquetes por rol

Las nuevas funciones de administración de paquetes proporcionan dos ámbitos para instalar y usar paquetes en SQL Server en una base de datos determinada:

- **Ámbito compartido**

  *Ámbito compartido* significa que los usuarios que le ha concedido permiso a la función de ámbito compartido (`rpkgs-shared`) pueden instalar y desinstalar paquetes a una base de datos especificada. Un paquete que se instala en una biblioteca de ámbito compartido lo pueden usar otros usuarios de la base de datos en SQL Server, siempre y cuando estos usuarios tengan permiso para usar paquetes de R instalados.

- **Ámbito privado**

  *Ámbito privado* significa que los usuarios que se han proporcionado con pertenencia en el rol de ámbito privado (`rpkgs-private`) puede instalar o desinstalar paquetes en una ubicación de biblioteca privada definida por el usuario. Por lo tanto, los paquetes instalados en el ámbito privado solo los puede usar el usuario que los instaló. Dicho de otra manera, un usuario de SQL Server no puede usar los paquetes privados que instaló otro usuario.

Estos modelos de ámbito *compartido* y *privado* se pueden combinar para desarrollar sistemas seguros personalizados para implementar y administrar paquetes en SQL Server.

Por ejemplo, con el ámbito compartido, el jefe o el administrador de un grupo de científicos de datos podría recibir permiso para instalar paquetes, que luego podrían usar el resto de los usuarios o de los científicos de datos en la misma instancia de SQL Server.

En otro escenario se podría necesitar más aislamiento entre los usuarios o se tendrían que usar diferentes versiones de paquetes. En ese caso, el ámbito privado se puede usar para asignar permisos a los científicos de datos, que se encargarían de instalar y usar únicamente los paquetes que necesitan. Dado que los paquetes se instalan para cada usuario, los paquetes que instale un usuario no afectarán al trabajo del resto de los usuarios que usan la misma base de datos de SQL Server.

### <a name="synchronizing-r-package-libraries"></a>Sincronización de las bibliotecas de paquete de R

La versión 2.0 de CTP de SQL Server 2017 (y la versión de abril de 2017 de Microsoft R Server) incluye nuevas funciones de R para *sincronizar paquetes*.

Sincronización de paquete significa que el motor de base de datos realiza un seguimiento de los paquetes que usan un propietario específico y un grupo y pueden escribir estos paquetes en el sistema de archivos si es necesario. Puede utilizar la sincronización de paquete en estos escenarios:

+ Desea mover los paquetes de R entre instancias de SQL Server
+ Tiene que volver a instalar los paquetes para un usuario específico o grupo después de restaura una base de datos

Para obtener más información, consulte [rxSyncPackages](../r/package-install-uninstall-and-sync.md).

## <a name="examples"></a>Ejemplos

Esos ejemplos demuestran el uso básico de las funciones de administración del paquete. Para ejecutar estos comandos requiere que tenga permiso para ejecutar comandos de R en la instancia.

+ Cuando se ejecuta desde un terminal de R remoto, se crea un objeto de contexto de cálculo especifica una instancia de SQL Server y, a continuación, ejecutan las funciones, pasando el contexto de proceso como un argumento.

+ Para ejecutar las funciones de administración del paquete desde un procedimiento almacenado, debe incluir en una llamada a `sp_execute_external_script`.

### <a name="package-scoping"></a>Ámbito de paquete

Este ejemplo se comprueba para los paquetes que se instalaron en la instancia `myServer`, en la base de datos `TestDB`. Administración de paquetes se limita a una base de datos específica y el usuario. Si el usuario no se especifica, se supone que el usuario que ejecuta la llamada de contexto de proceso. Para obtener más información, consulte [Scoping de paquetes por rol](#bkmk_scope).

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-location-on-a-remote-sql-server-compute-context"></a>Obtener la ubicación del paquete en un contexto de proceso de SQL Server remoto

En este ejemplo se obtiene la ruta de acceso del paquete **RevoScaleR** en el contexto del proceso, *sqlServer*.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>Obtener la ubicación de varios paquetes

En el ejemplo siguiente se obtienen las rutas de acceso de los paquetes **RevoScaleR** y **lattice** en el contexto de proceso, *sqlServer*. Para obtener información acerca de varios paquetes, pase un vector de cadena que contiene los nombres de paquete.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```

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

### <a name="get-package-versions-on-a-remote-compute-context"></a>Obtener las versiones del paquete en un contexto de proceso remoto.

Ejecute este comando desde una consola de R para obtener el número de compilación y los números de versión para los paquetes instalados en el contexto de proceso, *sqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Instalar un paquete en SQL Server

En este ejemplo se instala el paquete **ggplot2** y sus dependencias en el contexto de proceso, *sqlServer*.

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

### <a name="package-synchronization"></a>Sincronización de paquetes

En el ejemplo siguiente se sincroniza los paquetes instalados en el sistema de archivos con la lista de paquetes que se administran en la base de datos. Si faltan algunos paquetes, se instalan en el sistema de archivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="next-steps"></a>Pasos siguientes

[Cómo habilitar o deshabilitar la administración de paquetes de R](../r/r-package-how-to-enable-or-disable.md)

