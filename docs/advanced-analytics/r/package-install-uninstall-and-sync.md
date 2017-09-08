---
title: "Paquete de instalación, desinstalación y sincronizar | Documentos de Microsoft"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 959282395d178a090a3d447769ced4dca8882f89
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>Sincronización de paquetes de R para SQL Server

SQL Server de 2017 CTP 2.0 incluye una nueva función para la sincronización de los paquetes de R, para admitir la copia de seguridad y restauración de las recopilaciones de paquetes de R asociadas con las bases de datos de SQL Server. Esta característica ayuda a garantizar que los conjuntos complejos de los paquetes de R creados por los usuarios no se pierden y se pueden restaurar fácilmente.  

Este tema describe lo que hace la característica de sincronización de paquete y cómo usar el `rxSyncPackages()` función para realizar las tareas siguientes:

+  Sincronizar una lista de paquetes para una base de datos completa de SQL Server
+  Paquetes de sincronizar utilizados por un usuario individual o un grupo de usuarios

> [!NOTE]
> Esta función se proporciona como parte del software de versión preliminar y está sujeta a cambios antes de la versión final.

## <a name="what-is-package-synchronization"></a>¿Qué es la sincronización de paquetes 

Sincronización de paquetes es una nueva característica que funciona en particular con SQL Server contextos de proceso. Está diseñado para obtener una lista de paquetes de R que se instalan en una base de datos determinado, para un usuario o grupo concreto, y asegúrese de que los paquetes aparecen en la coincidencia de sistema de archivo los de la base de datos. 

Esto es útil si necesita mover una base de datos de usuario y mover los paquetes junto con la base de datos. También puede utilizar la sincronización de paquete cuando se copia de seguridad y restaurar una base de datos de SQL Server que se utiliza para los trabajos de R.

Sincronización de paquetes usa una función nueva, `rxSyncPackages()`. Para sincronizar la lista de paquetes, abra un símbolo del sistema de R, pase el contexto de proceso que define la instancia y la base de datos que desea trabajar con y, a continuación, proporcionar un ámbito de paquete o un nombre de usuario o propietario. 

### <a name="how-packages-are-managed-in-r-and-sql-server"></a>¿Cómo se administran los paquetes de R y SQL Server

Normalmente, cuando se ejecutan scripts de R con herramientas estándares de R, paquetes de R se instalan en el sistema de archivos. Si varias personas utilizan R en el mismo equipo, puede haber varias copias de los mismos paquetes, en carpetas diferentes o en bibliotecas de usuario diferente.

Sin embargo, para usar un paquete de R desde SQL Server, el paquete debe instalarse en la biblioteca de R predeterminado que está asociada a la instancia. Un equipo de servidor puede hospedar varias instancias de SQL Server con R habilitado y, en este caso, cada instancia puede tener un conjunto independiente de paquetes de R. 

El Administrador de base de datos es responsable de instalar paquetes en la instancia. Sin embargo, con las bibliotecas de administración del paquete, el administrador puede delegar esta responsabilidad a los usuarios. 

+ Para cada base de datos, el administrador puede proporcionar a los usuarios la capacidad de libremente instalar los paquetes de R que necesitan. Este mecanismo garantiza que varios usuarios pueden instalar diferentes versiones de paquetes de R sin causar conflictos para otros usuarios del equipo de SQL Server. Los usuarios individuales pueden instalar paquetes de para su propio uso, con una ubicación de sistema de archivos marcada como **privada**, si pertenecen a la función de base de datos **rpkgs privada**.

+ El administrador puede configurar un grupo de usuarios de paquete en una base de datos e instalar los paquetes que se comparten entre todos los usuarios del grupo. Los paquetes se pueden compartir entre los miembros del rol de base de datos **rpkgs compartidos**. Estos usuarios también pueden instalar paquetes a ubicaciones de ámbito privado. 

### <a name="goal-of-package-synchronization"></a>Objetivo de la sincronización de paquetes

Si una base de datos en un servidor se pierde o se debe mover, mediante la sincronización de paquete, puede restaurar conjuntos de paquetes específicos a una base de datos, el usuario o el grupo. 

La información sobre los usuarios y los paquetes que han instalado se almacena en la instancia de SQL Server y se utiliza para actualizar los paquetes en el sistema de archivos. Cada vez que agregue un nuevo paquete mediante las funciones de administración del paquete, se actualizan los registros de ambos en SQL Server y el sistema de archivos. Por lo tanto, si un usuario se mueve a otro SQL Server, puede realizar una copia de seguridad de base de datos de trabajo del usuario y restaurarla en el nuevo servidor y los paquetes para el usuario se instalarán en el sistema de archivos en el nuevo servidor, según sea necesario mediante R.


### <a name="supported-versions"></a>Versiones admitidas

Esta función se incluye en SQL Server de 2017 CTP 2.0.

Dado que esta función es parte de Microsoft R versión 9.1.0, esta característica se puede agregar a una instancia de SQL Server 2016 mediante la actualización de la instancia para que utilice la versión más reciente de Microsoft R. Para obtener más información, consulte [SqlBindR.exe Use para actualizar SQL Server R Services](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="to-synchronize-packages"></a>Para sincronizar los paquetes

Se llama a `rxSyncPackages` después de restaurar una instancia de SQL Server a un nuevo equipo, o si un R el paquete en el sistema de archivos; se parece estar dañada.

Si el comando se ejecuta correctamente, los paquetes existentes en el sistema de archivos se agregan a la base de datos, el ámbito y el propietario de acuerdo con lo especificado. Si el sistema de archivos está dañado, los paquetes son restred basándose en la lista que se mantiene en la base de datos.

### <a name="syntax"></a>Sintaxis
`rxSyncPackages(computeContext = rxGetOption("computeContext"),  scope = c("shared", "private"), owner = c(), verbose = getOption("verbose"))`

+ Contexto de proceso

    Definir un contexto de proceso de SQL Server, que consta de una instancia y base de datos y los paquetes que se va a sincronizar. Crear el contexto de servidor SQ mediante el `RxInSqlServer` función. Si no se especifica un contexto de proceso, se utiliza el contexto del proceso actual. 

+ Ámbito

  Indicar si va a instalar los paquetes de un solo usuario o para un grupo de usuarios: 

    + **privada** la operación incluirá solo los paquetes que se han instalado para su uso por un propietario especificado.
    + **compartido** el oepration incluirá todos los paquetes instalados para un grupo de usuarios. 

  Si ejecuta la función sin especificar ámbito privado o compartido, se aplican ambos ámbitos. Como resultado, se copiará todo el conjunto de paquetes disponibles para todos los ámbitos y los usuarios.

+ Propietario 

    Especifique el propietario de los paquetes que se va a sincronizar. El nombre del propietario debe ser un usuario de base de datos SQL válido. Si se deja vacío, se utiliza el nombre de usuario de inicio de sesión SQL especificada en la conexión.


### <a name="requirements"></a>Requisitos

+ La persona que ejecuta la función debe ser una entidad de seguridad en la instancia de SQL Server y la base de datos que tiene los paquetes y debe ser un miembro de un rol de administración del paquete: **compartido rpkgs** o **rpkgs privado** 
  + Para sincronizar los paquetes marcados como **compartido**, la persona que ejecuta la función debe ser miembro de la **rpkgs compartidos** rol y los paquetes que se están moviendo deben haberse instalado para un compartido biblioteca de ámbito.
  + Para sincronizar los paquetes marcados como **privada**, ya sea el propietario del paquete o el administrador debe ejecutar la función y los paquetes deben ser privados.
+ **usuarios rpkgs** -miembros de este rol pueden ejecutar código que usa paquetes instalados en la instancia de SQL Server, pero no se puede instalar o paquetes de sincronización.
+ Para sincronizar los paquetes en nombre de otros usuarios, el propietario debe ser un miembro de la **db_owner** rol de base de datos.

## <a name="examples"></a>Ejemplos

Los ejemplos siguientes crear una conexión a una instancia específica de SQL Server, especifican una base de datos y, a continuación, especifican un conjunto de paquetes que se va a sincronizar. 

Cuando la llamada a `rxSyncPackages` se realiza, el paquete de las listas están sincronizadas entre el sistema de archivos y la base de datos. 

### <a name="synchronize-all-by-database"></a>Sincronizar todas las bases de datos

Este ejemplo obtiene todos los paquetes instalados en la base de datos [TestDB]. Dado que no es específico de ningún propietario, la lista incluye todos los paquetes que se han instalado para ámbitos privados como compartidos.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-scope"></a>Restringir paquetes sincronizados por ámbito 

El siguiente sincronizar ejemplos solo los paquetes en el ámbito compartido o ámbito privado.

**Ámbito compartido**

```R
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)
```

**Ámbito privado**

```R
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-owner"></a>Restringir paquetes sincronizados por propietario 

En el ejemplo siguiente se muestra cómo obtener solo los paquetes que se han instalado para un usuario específico. En este ejemplo, el usuario se identifica mediante el nombre de inicio de sesión SQL, *user1*.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="see-also"></a>Vea también

[Administración de paquetes de R para SQL Server](../r/r-package-management-for-sql-server-r-services.md)
