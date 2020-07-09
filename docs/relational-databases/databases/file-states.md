---
title: Estados de los archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1a58f92ebb7e6c59d80277cc17457927cff01ff8
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002955"
---
# <a name="file-states"></a>Estados de los archivos
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el estado de un archivo de bases de datos se mantiene independientemente del estado de la base de datos. Un archivo siempre está en un estado específico, como ONLINE o OFFLINE. Para ver el estado actual de un archivo, use la vista de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) o [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) . Si la base de datos está sin conexión, el estado de los archivos se puede ver desde la vista de catálogo [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) .  
  
 El estado de los archivos en un grupo de archivos determina la disponibilidad de todo el grupo de archivos. Para que un grupo de archivos esté disponible, todos los archivos del grupo de archivos deben estar en línea. Para ver el estado actual de un grupo de archivos, utilice la vista de catálogo [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md) . Si un grupo de archivos está sin conexión e intenta tener acceso al grupo de archivos mediante una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] , devolverá un error. Cuando el optimizador de consultas crea planes para instrucciones SELECT, evita índices no clúster y vistas indizadas que residen en grupos de archivos sin conexión, permitiendo que estas instrucciones tengan éxito. No obstante, si el grupo de archivos sin conexión contiene el montón o el índice clúster de la tabla de destino, las instrucciones SELECT no funcionarán. Adicionalmente, cualquier instrucción INSERT, UPDATE o DELETE que modifique una tabla con cualquier índice en un grupo de archivos sin conexión no funcionará.  
  
## <a name="file-state-definitions"></a>Definiciones de estado de los archivos  
 En la siguiente tabla se definen los estados de los archivos.  
  
|State|Definición|  
|-----------|----------------|  
|ONLINE|El archivo está disponible para todas las operaciones. Los archivos del grupo de archivos principal siempre están en línea si la base de datos lo está. Si un archivo del grupo de archivos principal no está en línea, la base de datos no está en línea y los estados de los archivos secundarios no están definidos.|  
|OFFLINE|El archivo no está disponible para su acceso y puede no estar presente en el disco. Los archivos pasan a estar sin conexión por una acción explícita del usuario y permanecen sin conexión hasta que se produce una acción adicional del usuario.<br /><br /> **\*\* Precaución \*\*** Un archivo solo tiene que establecerse como sin conexión cuando está dañado, pero se puede restaurar. Un archivo que está sin conexión solo se puede poner en línea restaurándolo de la copia de seguridad. Para obtener más información sobre cómo restaurar un único archivo, vea [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md). <br /><br /> Un archivo de base de datos también se establece como OFFLINE cuando una base de datos se encuentra en un estado de recuperación de registros masiva o completa y se descarta un archivo. La entrada de sys.master_files persiste hasta que un registro de transacciones se trunca más allá del valor drop_lsn. Para obtener más información, vea [Truncamiento del registro de transacciones](../../relational-databases/logs/the-transaction-log-sql-server.md#Truncation). |  
|RESTORING|Se está restaurando el archivo. Los archivos entran en el estado de restauración a causa de un comando de restauración que afecta a todo el archivo y permanecen en ese estado hasta que se completa la restauración y se recupera el archivo.|  
|RECOVERY PENDING|Se ha pospuesto la recuperación del archivo. Un archivo entra en este estado automáticamente a causa de un proceso de restauración por etapas en el que el archivo no se restaura ni recupera. Se necesita una acción adicional por parte del usuario para resolver el error y permitir que se complete el proceso de recuperación. Para obtener más información, vea [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md).|  
|SUSPECT|La recuperación del archivo no ha sido correcta durante un proceso de restauración en línea. Si el archivo está en el grupo de archivos principal, la base de datos también se marca como sospechosa. De lo contrario, solo es sospechoso el archivo y la base de datos sigue estando en línea.<br /><br /> El archivo permanecerá en el estado sospechoso hasta que esté disponible mediante uno de los siguientes métodos:<br /><br /> Restauración y recuperación<br /><br /> DBCC CHECKDB con REPAIR_ALLOW_DATA_LOSS|  
|DEFUNCT|El archivo se quitó cuando no estaba en línea. Todos los archivos de un grupo de archivos pasan a estar inactivos cuando se quita un grupo de archivos sin conexión.|  
  
## <a name="related-content"></a>Contenido relacionado  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [Estados de base de datos](../../relational-databases/databases/database-states.md)  
  
 [Estados de creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
 [Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md)  
