---
title: Estados de los archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- restoring file state [SQL Server]
- verifying file states
- current file states
- verifying filegroup states
- file states [SQL Server]
- online file state
- offline file state [SQL Server]
- viewing filegroup states
- viewing file states
- suspect file state
- recovering file state [SQL Server]
- current filegroup state
- recovery pending file state [SQL Server]
- displaying file states
- states [SQL Server], files
- displaying filegroup states
- defunct file state
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc37fbade038b39d6d05cb5b51ecc3e8ba405e2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871578"
---
# <a name="file-states"></a>Estados de los archivos
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el estado de un archivo de bases de datos se mantiene independientemente del estado de la base de datos. Un archivo siempre está en un estado específico, como ONLINE o OFFLINE. Para ver el estado actual de un archivo, use la vista de catálogo [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) o [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) . Si la base de datos está sin conexión, el estado de los archivos se puede ver desde la vista de catálogo [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) .  
  
 El estado de los archivos en un grupo de archivos determina la disponibilidad de todo el grupo de archivos. Para que un grupo de archivos esté disponible, todos los archivos del grupo de archivos deben estar en línea. Para ver el estado actual de un grupo de archivos, utilice la vista de catálogo [sys.filegroups](/sql/relational-databases/system-catalog-views/sys-filegroups-transact-sql) . Si un grupo de archivos está sin conexión e intenta tener acceso al grupo de archivos mediante una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] , devolverá un error. Cuando el optimizador de consultas crea planes para instrucciones SELECT, evita índices no clúster y vistas indizadas que residen en grupos de archivos sin conexión, permitiendo que estas instrucciones tengan éxito. No obstante, si el grupo de archivos sin conexión contiene el montón o el índice clúster de la tabla de destino, las instrucciones SELECT no funcionarán. Adicionalmente, cualquier instrucción INSERT, UPDATE o DELETE que modifique una tabla con cualquier índice en un grupo de archivos sin conexión no funcionará.  
  
## <a name="file-state-definitions"></a>Definiciones de estado de los archivos  
 En la siguiente tabla se definen los estados de los archivos.  
  
|State|Definición|  
|-----------|----------------|  
|ONLINE|El archivo está disponible para todas las operaciones. Los archivos del grupo de archivos principal siempre están en línea si la base de datos lo está. Si un archivo del grupo de archivos principal no está en línea, la base de datos no está en línea y los estados de los archivos secundarios no están definidos.|  
|OFFLINE|El archivo no está disponible para su acceso y puede no estar presente en el disco. Los archivos pasan a estar sin conexión por una acción explícita del usuario y permanecen sin conexión hasta que se produce una acción adicional del usuario.<br /><br /> **\*\* Precaución \*\*** Un archivo solo debe establecerse como sin conexión cuando está dañado pero se puede restaurar. Un archivo que está sin conexión solo se puede poner en línea restaurándolo de la copia de seguridad. Para obtener más información sobre cómo restaurar un único archivo, vea [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).|  
|RESTORING|Se está restaurando el archivo. Los archivos entran en el estado de restauración a causa de un comando de restauración que afecta a todo el archivo y permanecen en ese estado hasta que se completa la restauración y se recupera el archivo.|  
|RECOVERY PENDING|Se ha pospuesto la recuperación del archivo. Un archivo entra en este estado automáticamente a causa de un proceso de restauración por etapas en el que el archivo no se restaura ni recupera. Se necesita una acción adicional por parte del usuario para resolver el error y permitir que se complete el proceso de recuperación. Para obtener más información, vea [Restauraciones por etapas &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md).|  
|SUSPECT|La recuperación del archivo no ha sido correcta durante un proceso de restauración en línea. Si el archivo está en el grupo de archivos principal, la base de datos también se marca como sospechosa. De lo contrario, solo es sospechoso el archivo y la base de datos sigue estando en línea.<br /><br /> El archivo permanecerá en el estado sospechoso hasta que esté disponible mediante uno de los siguientes métodos:<br /><br /> Restauración y recuperación<br /><br /> DBCC CHECKDB con REPAIR_ALLOW_DATA_LOSS|  
|DEFUNCT|El archivo se quitó cuando no estaba en línea. Todos los archivos de un grupo de archivos pasan a estar inactivos cuando se quita un grupo de archivos sin conexión.|  
  
## <a name="related-content"></a>Contenido relacionado  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [Estados de base de datos](database-states.md)  
  
 [Estados de creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [Archivos y grupos de archivos de base de datos](database-files-and-filegroups.md)  
  
  
