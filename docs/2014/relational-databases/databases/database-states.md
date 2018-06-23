---
title: Estados de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4ad323cffec4772208aa71a5088f2eacc536896e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204400"
---
# <a name="database-states"></a>Estados de base de datos
  Una base de datos siempre está en un estado específico. Por ejemplo, esos estados pueden ser ONLINE, OFFLINE o SUSPECT. Para comprobar el estado actual de una base de datos, seleccione la columna **state_desc** de la vista de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) o la propiedad **Status** en la función [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) .  
  
## <a name="database-state-definitions"></a>Definiciones de estados de la base de datos  
 En la siguiente tabla se define los estados de la base de datos.  
  
|State|Definición|  
|-----------|----------------|  
|ONLINE|La base de datos está disponible para su acceso. El grupo de archivos principal está en línea, aunque la fase de deshacer de la recuperación puede no haberse completado.|  
|OFFLINE|La base de datos no está disponible. Una base de datos pasa a estar sin conexión por la acción explícita del usuario y permanece sin conexión hasta que el usuario toma otra acción. Por ejemplo, la base de datos puede dejarse sin conexión para mover un archivo a un nuevo disco. La base de datos se vuelve a poner en línea una vez completado el traslado.|  
|RESTORING|Uno o varios archivos del grupo de archivos principal se está restaurando, o uno o varios archivos secundarios se están restaurando sin conexión. La base de datos no está disponible.|  
|RECOVERING|Se está recuperando la base de datos. El proceso de recuperación es un estado transitorio, la base de datos se pone automáticamente en línea si la recuperación tiene éxito. Si la recuperación no tiene éxito, la base de datos pasa a ser sospechosa. La base de datos no está disponible.|  
|RECOVERY PENDING|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha encontrado un error relacionado con un recurso durante la recuperación. La base de datos no está dañada pero pueden faltar archivos o bien limitaciones de recursos del sistema pueden estar impidiendo que se inicie. La base de datos no está disponible. Se necesita una acción adicional por parte del usuario para resolver el error y permitir que se complete el proceso de recuperación.|  
|SUSPECT|Como mínimo un grupo de archivos principal es sospechoso y puede estar dañado. La base de datos no se puede recuperar durante el inicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La base de datos no está disponible. Se requiere una acción adicional por parte del usuario para resolver el problema.|  
|EMERGENCY|El usuario ha cambiado la base de datos y ha establecido el estado en EMERGENCY. La base de datos está en modo de usuario único y se puede reparar o restaurar. La base de datos está marcada como READ_ONLY, el registro está deshabilitado y el acceso está limitado a miembros del rol fijo de servidor **sysadmin** . EMERGENCY se utiliza principalmente para la solución de problemas. Por ejemplo, una base de datos marcada como sospechosa se puede establecer en el estado EMERGENCY. Esto puede permitir al administrador del sistema acceso de solo lectura a la base de datos. Solo los miembros del rol fijo de servidor **sysadmin** pueden establecer una base de datos en el estado EMERGENCY.|  
  
## <a name="related-content"></a>Contenido relacionado  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [Estados de creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [Estados de los archivos](file-states.md)  
  
  
