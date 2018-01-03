---
title: "Sincronización de paquetes de R para SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 10/02/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7530d67c2c74b4918228ea91597f1667c0abbd6
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronización de paquetes de R para SQL Server

SQL Server 2017 incluye la capacidad de sincronizar colecciones de paquetes de R entre el sistema de archivos y la instancia y base de datos que se empleen los paquetes.
Esta característica se proporciona para que resulten más fáciles de realizar copias de seguridad de las colecciones de paquete de R asociadas con las bases de datos de SQL Server. Con esta característica, un administrador puede restaurar no solo la base de datos, pero los paquetes de R que se usaron los científicos de datos trabaja en esa base de datos.

Este tema describe la característica de sincronización de paquete y cómo usar el [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages) función para realizar las tareas siguientes:

+ Sincronizar una lista de paquetes para una base de datos completa de SQL Server

+ Sincronizar los paquetes utilizados por un usuario individual o un grupo de usuarios

+ Si un usuario se mueve a otro SQL Server, puede realizar una copia de seguridad de base de datos de trabajo del usuario y restaurarla en el nuevo servidor, y los paquetes para el usuario se instalarán en el sistema de archivos en el nuevo servidor, según sea necesario mediante R.

Por ejemplo, podría utilizar la sincronización de paquete en estos escenarios:

+ El DBA ha restaurado una instancia de SQL Server a un nuevo equipo y pedir a los usuarios para conectarse desde sus clientes de R y ejecute `rxSyncPackages` para actualizar y restaurar sus paquetes.

+ Cree un paquete de R en el sistema de archivos está dañado para ejecutar `rxSyncPackages` en SQL Server.

## <a name="requirements"></a>Requisitos

Antes de que se puede utilizar la sincronización de paquete, se debe tener la versión adecuada de Microsoft R y tener habilitada la característica de base de datos relacionada.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinar si el servidor es compatible con la administración de paquetes

Esta característica está disponible en SQL Server de 2017 CTP 2 o posterior.

Dado que esta característica utiliza funciones de R en Microsoft R versión 9.1.0, esta característica se puede agregar a una instancia de SQL Server 2016 mediante la actualización de la instancia para que utilice la versión más reciente de Microsoft R. Para obtener más información, consulte [SqlBindR.exe Use para actualizar SQL Server R Services](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="enable-the-package-management-feature"></a>Habilitar la característica de administración de paquetes

Para utilizar la sincronización del paquete requiere que las nuevas características de administración del paquete esté habilitado en la instancia de SQL Server y en bases de datos individuales que utiliza para ejecutar tareas de R.

1. El administrador del servidor, habilita la característica de la instancia de SQL Server.
2. Para cada base de datos, el administrador concede a los usuarios la posibilidad de instalar o compartir paquetes de R.

Cuando esto sucede, se almacena información sobre los usuarios y los paquetes que han instalado en la instancia de SQL Server. A continuación, se puede aplicar esta información para actualizar los paquetes de R en el sistema de archivos.

Cada vez que agregue un nuevo paquete mediante las funciones de administración del paquete, se actualizan los registros de ambos en SQL Server y el sistema de archivos.

> [!NOTE]
> No se puede utilizar la sincronización de paquete si ha sido instalando paquetes de R la forma tradicional, con herramientas de R para instalar paquetes directamente en el sistema de archivos.
### <a name="permissions"></a>Permissions

+ La persona que ejecuta la función de sincronización de paquete debe ser una entidad en la instancia de SQL Server y la base de datos con los paquetes de seguridad.

+ El llamador de la función debe ser un miembro de uno de estos roles de administración del paquete: **compartido rpkgs** o **rpkgs privada**.

+ Para sincronizar los paquetes marcados como **compartido**, la persona que ejecuta la función debe ser miembro de la **rpkgs compartidos** rol y los paquetes que se están moviendo deben haberse instalado para un compartido biblioteca de ámbito.

+ Para sincronizar los paquetes marcados como **privada**, ya sea el propietario del paquete o el administrador debe ejecutar la función y los paquetes deben ser privados.

+ Para sincronizar los paquetes en nombre de otros usuarios, el propietario debe ser un miembro de la **db_owner** rol de base de datos.

## <a name="how-package-synchronization-works"></a>Cómo funciona la sincronización de paquete

Para utilizar la sincronización de paquete, llame a [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que es una función nueva en [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler). Puede llamar a esta función desde SQL Server mediante sp_execute_external_script, o puede ejecutarlo desde un cliente remoto de R y especificar el contexto de proceso de SQL Server. 

Puesto que los paquetes se administran en el nivel de base de datos, para cada llamada a `rxSyncPackages`, debe especificar una instancia de SQL Server y base de datos y, a continuación, enumerar los paquetes, o especifique el ámbito del paquete.

1. Crear el contexto de proceso de SQL Server mediante el `RxInSqlServer` función. Si no se especifica un contexto de proceso, se utiliza el contexto del proceso actual.

2. Proporcione el nombre de una base de datos en la instancia en el contexto de proceso especificado. Los paquetes se administran por base de datos.

3. Enumerar los paquetes que se va a sincronizar.

4.  También puede utilizar el *ámbito* argumento para indicar si va a sincronizar los paquetes de un solo usuario o para un grupo de usuarios. Si ejecuta la función sin especificar **privada** o **compartido** establecer el ámbito, todo el conjunto de paquetes disponibles para todos los ámbitos y los usuarios que se va a copiar.

Si el comando se ejecuta correctamente, los paquetes existentes en el sistema de archivos se agregan a la base de datos, con el ámbito especificado y el propietario. Si el sistema de archivos está dañado, se restauran los paquetes en función de la lista mantenida en la base de datos.

### <a name="example-1-synchronize-all-package-by-database"></a>Ejemplo 1. Sincronizar todos los paquetes mediante la base de datos

Este ejemplo obtiene todos los paquetes instalados en la base de datos [TestDB]. Dado que no es específico de ningún propietario, la lista incluye todos los paquetes que se han instalado para ámbitos privados como compartidos.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>Ejemplo 2. Restringir paquetes sincronizados por ámbito

Los ejemplos siguientes sincronizan solo los paquetes en el ámbito especificado.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Ejemplo 3. Restringir paquetes sincronizados por propietario

En el ejemplo siguiente se muestra cómo obtener solo los paquetes que se han instalado para un usuario específico. En este ejemplo, el usuario se identifica mediante el nombre de inicio de sesión SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

### <a name="example-4-restrict-synchronized-packages-by-owner"></a>Ejemplo 4. Restringir paquetes sincronizados por propietario

En el ejemplo siguiente se sincroniza los paquetes instalados en el sistema de archivos con la lista de paquetes que se administran en la base de datos. Si los paquetes no está presente, se instala en el sistema de archivos.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="related-resources"></a>Recursos relacionados

[Administración de paquetes de R para SQL Server](r-package-management-for-sql-server-r-services.md)
