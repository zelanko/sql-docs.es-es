---
title: 'Sincronización de paquetes de R desde el sistema de archivos: SQL Server Machine Learning Services'
description: Actualizar las bibliotecas de R en SQL Server con las versiones más recientes instaladas en el sistema de archivos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f6782acd011242cfd9b8ed4fe24a11fba85e932c
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140519"
---
# <a name="r-package-synchronization-for-sql-server"></a>Sincronización de paquetes de R para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La versión de RevoScaleR incluida en SQL Server 2017 incluye la capacidad de sincronizar las colecciones de paquetes de R entre el sistema de archivos y la instancia y base de datos que donde se usan los paquetes.

Esta característica se proporciona para facilitar la copia de seguridad de las colecciones de paquete de R asociadas con las bases de datos de SQL Server. Con esta característica, un administrador puede restaurar no solo la base de datos, pero los paquetes de R que se usaron los científicos de datos trabajar en esa base de datos.

Este artículo describe la característica de sincronización de paquete y cómo usar el [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) función para realizar las tareas siguientes:

+ Sincronizar una lista de paquetes para una base de datos completa de SQL Server

+ Sincronizar los paquetes utilizados por un usuario individual, o por un grupo de usuarios

+ Si un usuario se mueve a otro SQL Server, puede realizar una copia de seguridad de base de datos de trabajo del usuario y restaurarla en el nuevo servidor, y los paquetes para el usuario se instalarán en el sistema de archivos en el nuevo servidor, según sea necesario por R.

Por ejemplo, puede usar la sincronización de paquetes en estos escenarios:

+ El DBA restaurado una instancia de SQL Server a un nuevo equipo y pide a los usuarios conectarse desde los clientes de R y ejecute `rxSyncPackages` para actualizar y restaurar sus paquetes.

+ Cree un paquete de R en el sistema de archivos está dañado por lo que ejecutar `rxSyncPackages` en SQL Server.

## <a name="requirements"></a>Requisitos

Para poder usar la sincronización de paquetes, debe tener la versión adecuada de Microsoft R o Machine Learning Server. Esta característica se proporciona en Microsoft R versión 9.1.0 o posterior. 

También debe habilitar la [característica de administración de paquetes](r-package-how-to-enable-or-disable.md) en el servidor.

### <a name="determine-whether-your-server-supports-package-management"></a>Determinar si el servidor admite la administración de paquetes

Esta característica está disponible en SQL Server 2017 CTP 2 o posterior.

Esta característica se puede agregar a una instancia de SQL Server 2016 mediante la actualización de la instancia para usar la versión más reciente de Microsoft R. Para obtener más información, consulte [usar SqlBindR.exe para actualizar SQL Server R Services](../install/upgrade-r-and-python.md).

### <a name="enable-the-package-management-feature"></a>Habilitar la característica de administración de paquetes

Para usar la sincronización del paquete requiere que la nueva característica de administración del paquete esté habilitado en la instancia de SQL Server y en bases de datos individuales. Para obtener más información, consulte [habilitar o deshabilitar la administración de paquetes de SQL Server](r-package-how-to-enable-or-disable.md).

1. El administrador del servidor, habilita la característica para la instancia de SQL Server.
2. Para cada base de datos, el administrador concede individuales a los usuarios la capacidad de instalar o compartir paquetes de R, mediante roles de base de datos.

Cuando esto sucede, puede usar las funciones de RevoScaleR, como [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) para instalar paquetes en una base de datos.  Se almacena información acerca de los usuarios y los paquetes que pueden usar en la instancia de SQL Server. 

Siempre que agregue un nuevo paquete mediante las funciones de administración de paquetes, tanto los registros en SQL Server y el sistema de archivos se actualizan. Esta información puede utilizarse para restaurar la información de paquete para la base de datos completa.

### <a name="permissions"></a>Permisos

+ La persona que ejecuta la función de sincronización de paquete debe ser una entidad en la instancia de SQL Server y base de datos con los paquetes de seguridad.

+ El llamador de la función debe ser un miembro de uno de estos roles de administración del paquete: **rpkgs-shared** o **rpkgs-private**.

+ Para sincronizar los paquetes marcados como **compartido**, la persona que se está ejecutando la función deben pertenecer a la **rpkgs-shared** rol y los paquetes que se están moviendo deben haberse instalado para un compartido biblioteca de ámbito.

+ Para sincronizar los paquetes marcados como **privada**, ya sea el propietario del paquete o el administrador debe ejecutar la función y los paquetes deben ser privados.

+ Para sincronizar los paquetes en nombre de otros usuarios, el propietario debe ser un miembro de la **db_owner** rol de base de datos.

## <a name="how-package-synchronization-works"></a>Cómo funciona la sincronización de paquete

Para utilizar la sincronización de paquetes, llame a [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages), que es una función nueva en [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler). 

Para cada llamada a `rxSyncPackages`, debe especificar una instancia de SQL Server y base de datos. A continuación, puede enumerar los paquetes que se va a sincronizar o especificar el ámbito del paquete.

1. Crear el contexto de cálculo de SQL Server mediante el `RxInSqlServer` función. Si no se especifica un contexto de proceso, se usa el contexto de cálculo actual.

2. Proporcione el nombre de una base de datos en la instancia en el contexto de proceso especificado. Los paquetes se sincronizan por base de datos.

3. Especificar los paquetes que se va a sincronizar con el argumento de ámbito.

    Si usas **privada** se sincronizan ámbito, solo los paquetes que pertenezca al propietario especificado. Si especifica **compartido** ámbito, todos los paquetes no privados en la base de datos se sincronizan. 
    
    Si ejecuta la función sin especificar **privada** o **compartido** ámbito, se sincronizan todos los paquetes.

4. Si el comando es correcto, los paquetes existentes en el sistema de archivos se agregan a la base de datos, con el ámbito especificado y el propietario.

    Si el sistema de archivos está dañado, los paquetes se restauran en función de la lista mantenida en la base de datos.

    Si la característica de administración de paquetes no está disponible en la base de datos de destino, se produce un error: "La característica de administración de paquetes no está habilitada en el servidor SQL Server o versión es demasiado antigua"

### <a name="example-1-synchronize-all-package-by-database"></a>Ejemplo 1. Sincronizar todos los paquetes base de datos

Este ejemplo obtiene todos los paquetes nuevos desde el sistema de archivos local e instala los paquetes en la base de datos [TestDB]. Dado que no es específica de ningún propietario, la lista incluye todos los paquetes que se han instalado para ámbitos privados y se comparte.

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

El ejemplo siguiente muestra cómo sincronizar solo los paquetes que se han instalado para un usuario específico. En este ejemplo, el usuario se identifica mediante el nombre de inicio de sesión SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>Recursos relacionados

[Administración de paquetes de R para SQL Server](install-additional-r-packages-on-sql-server.md)
