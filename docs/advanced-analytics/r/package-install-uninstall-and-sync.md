---
title: Sincronización de paquetes de R desde el sistema de archivos
description: Actualice las bibliotecas de R en SQL Server con las versiones más recientes instaladas en el sistema de archivos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4e0b6133bcecc553934cd657785ea9ee765c6fd9
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715076"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronización de paquetes de R para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La versión de RevoScaleR que se incluye en SQL Server 2017 incluye la capacidad de sincronizar las colecciones de paquetes de R entre el sistema de archivos y la instancia y la base de datos donde se usan los paquetes.

Esta característica se ha proporcionado para facilitar la copia de seguridad de colecciones de paquetes de R asociadas a bases de datos de SQL Server. Con esta característica, un administrador puede restaurar no solo la base de datos, sino también los paquetes de R utilizados por los científicos de datos que trabajan en esa base de datos.

En este artículo se describe la característica de sincronización de paquetes y cómo usar la función [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) para realizar las siguientes tareas:

+ Sincronizar una lista de paquetes para una base de datos de SQL Server completa

+ Sincronizar paquetes usados por un usuario individual o por un grupo de usuarios

+ Si un usuario se mueve a otro SQL Server, puede realizar una copia de seguridad de la base de datos de trabajo del usuario y restaurarla en el nuevo servidor, y los paquetes del usuario se instalarán en el sistema de archivos del nuevo servidor, tal y como requiera R.

Por ejemplo, puede usar la sincronización de paquetes en estos escenarios:

+ El DBA restauró una instancia de SQL Server a una nueva máquina y pide a los usuarios que se conecten desde sus `rxSyncPackages` clientes de R y ejecuten para actualizar y restaurar sus paquetes.

+ Cree que un paquete de R en el sistema de archivos está dañado, por `rxSyncPackages` lo que se ejecuta en el SQL Server.

## <a name="requirements"></a>Requisitos

Para poder usar la sincronización de paquetes, debe tener la versión adecuada de Microsoft R o Machine Learning Server. Esta característica se proporciona en la versión 9.1.0 o posterior de Microsoft R. 

También debe habilitar la [característica de administración de paquetes](r-package-how-to-enable-or-disable.md) en el servidor.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinar si el servidor es compatible con la administración de paquetes

Esta característica está disponible en SQL Server 2017 CTP 2 o posterior.

Puede Agregar esta característica a una instancia de SQL Server 2016 mediante la actualización de la instancia de para que use la versión más reciente de Microsoft R. Para obtener más información, vea [usar SqlBindR. exe para actualizar SQL Server R Services](../install/upgrade-r-and-python.md).

### <a name="enable-the-package-management-feature"></a>Habilitar la característica de administración de paquetes

El uso de la sincronización de paquetes requiere que la nueva característica de administración de paquetes esté habilitada en la instancia de SQL Server y en las bases de datos individuales. Para obtener más información, vea [habilitar o deshabilitar la administración de paquetes para SQL Server](r-package-how-to-enable-or-disable.md).

1. El administrador del servidor habilita la característica para la instancia de SQL Server.
2. Para cada base de datos, el administrador concede a los usuarios individuales la capacidad de instalar o compartir paquetes de R mediante roles de base de datos.

Una vez hecho esto, puede usar las funciones de RevoScaleR, como [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) para instalar paquetes en una base de datos.  La información sobre los usuarios y los paquetes que pueden usar se almacena en la instancia de SQL Server. 

Siempre que se agrega un nuevo paquete mediante las funciones de administración de paquetes, se actualizan los registros de SQL Server y del sistema de archivos. Esta información se puede usar para restaurar información de paquetes para toda la base de datos.

### <a name="permissions"></a>Permisos

+ La persona que ejecuta la función de sincronización de paquetes debe ser una entidad de seguridad en la instancia de SQL Server y en la base de datos que contiene los paquetes.

+ El autor de la llamada de la función debe ser miembro de uno de estos roles de administración de paquetes: **rpkgs-Shared** o **rpkgs-Private**.

+ Para sincronizar los paquetesmarcados como compartidos, la persona que ejecuta la función debe ser miembro del rol **compartido rpkgs** y los paquetes que se van a migrar deben haberse instalado en una biblioteca de ámbitos compartidos.

+ Para sincronizar los paquetes marcados como **privados**, el propietario del paquete o el administrador deben ejecutar la función y los paquetes deben ser privados.

+ Para sincronizar los paquetes en nombre de otros usuarios, el propietario debe ser miembro del rol de base de datos **db_owner** .

## <a name="how-package-synchronization-works"></a>Cómo funciona la sincronización de paquetes

Para usar la sincronización de paquetes, llame a [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que es una nueva función de [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Para cada llamada a `rxSyncPackages`, debe especificar una instancia de SQL Server y una base de datos de. A continuación, enumere los paquetes que se van a sincronizar o especifique el ámbito del paquete.

1. Cree el contexto de cálculo de SQL Server mediante la `RxInSqlServer` función. Si no se especifica un contexto de cálculo, se usa el contexto de cálculo actual.

2. Proporcione el nombre de una base de datos en la instancia de en el contexto de proceso especificado. Los paquetes se sincronizan por base de datos.

3. Especifique los paquetes que se van a sincronizar mediante el argumento Scope.

    Si usa un ámbito **privado** , solo se sincronizan los paquetes que pertenecen al propietario especificado. Si especifica el ámbito **compartido** , se sincronizarán todos los paquetes no privados de la base de datos. 
    
    Si ejecuta la función sin especificar un ámbito **privado** o **compartido** , se sincronizarán todos los paquetes.

4. Si el comando se ejecuta correctamente, los paquetes existentes en el sistema de archivos se agregan a la base de datos, con el ámbito y el propietario especificados.

    Si el sistema de archivos está dañado, los paquetes se restauran en función de la lista que se mantiene en la base de datos.

    Si la característica de administración de paquetes no está disponible en la base de datos de destino, se produce un error: "La característica de administración de paquetes no está habilitada en el SQL Server o la versión es demasiado antigua".

### <a name="example-1-synchronize-all-package-by-database"></a>Ejemplo 1. Sincronizar todos los paquetes por base de datos

En este ejemplo se obtienen todos los paquetes nuevos del sistema de archivos local y se instalan los paquetes en la base de datos [TestDB]. Dado que ningún propietario es específico, la lista incluye todos los paquetes que se han instalado para ámbitos privados y compartidos.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>Ejemplo 2. Restringir paquetes sincronizados por ámbito

En los siguientes ejemplos se sincronizan solo los paquetes en el ámbito especificado.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>Ejemplo 3: Restringir paquetes sincronizados por propietario

En el ejemplo siguiente se muestra cómo sincronizar solo los paquetes que se instalaron para un usuario específico. En este ejemplo, el usuario se identifica mediante el nombre de inicio de sesión de SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Recursos relacionados

[Administración de paquetes de R para SQL Server](install-additional-r-packages-on-sql-server.md)
