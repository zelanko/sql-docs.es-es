---
title: Copias de seguridad de solo copia (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96267b98d7e17b920e0a7cee70b69e4c964584e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798011"
---
# <a name="copy-only-backups-sql-server"></a>Copias de seguridad de solo copia (SQL Server)
  Una *copia de seguridad de solo copia* es una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] independiente de la secuencia de copias de seguridad convencionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Normalmente, la realización de una copia de seguridad cambia la base de datos y afecta a la forma de restaurar las copias de seguridad posteriores. Sin embargo, a veces es útil realizar una copia de seguridad con un fin específico sin afectar a los procedimientos generales para copias de seguridad y restauración de la base de datos. Las copias de seguridad de solo copia sirven para este propósito.  
  
 Los tipos de copias de seguridad de solo copia son los siguientes:  
  
-   Copias de seguridad completas de solo copia (todos los modelos de recuperación)  
  
     Una copia de seguridad de solo copia no puede servir como base diferencial ni copia de seguridad diferencial y no afecta a la base diferencial.  
  
     El proceso de restauración de una copia de seguridad completa de solo copia es el mismo que la restauración de cualquier otra copia de seguridad completa.  
  
-   Copias de seguridad de registros de solo copia (solo modelo de recuperación completa y modelo de recuperación optimizado para cargas masivas de registros)  
  
     Una copia de seguridad de registros de solo copia mantiene el punto de archivo del registro existente y, por tanto, no afecta a la secuenciación de copias de seguridad de registros periódicas. Las copias de seguridad de registros de solo copia suelen ser innecesarias. En lugar de ello, puede crear una nueva copia de seguridad de registros rutinaria (con WITH NORECOVERY) y utilizarla junto con las copias de seguridad de registros anteriores que sean necesarias para la secuencia de restauración. Sin embargo, una copia de seguridad de registros de solo copia en ocasiones puede resultar útil para realizar una restauración en línea. Para ver un ejemplo, consulte [Ejemplo: restauración en línea de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md).  
  
     El registro de transacciones nunca se trunca después de una copia de seguridad de solo copia.  
  
 Las copias de seguridad de solo copia se registran en la columna **is_copy_only** de la tabla [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) .  
  
## <a name="to-create-a-copy-only-backup"></a>Para crear una copia de seguridad de solo copia  
 Para crear una copia de seguridad de solo copia, utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell.  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
1.  En la página **General** del cuadro de diálogo **Copia de seguridad de base de datos**, seleccione la opción **Copia de seguridad de solo copia**.  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 La sintaxis de [!INCLUDE[tsql](../../../includes/tsql-md.md)] necesaria es la siguiente:  
  
-   Para una copia de seguridad completa de solo copia:  
  
     *Database_name* de base de \<datos*>* de copia de seguridad para backup_device... CON COPY_ONLY...  
  
    > [!NOTE]  
    >  COPY_ONLY no tiene ningún efecto cuando se especifica con la opción DIFFERENTIAL.  
  
-   Para una copia de seguridad de registros de solo copia:  
  
     *Database_name* del registro de *\<* copia*>* de seguridad para backup_device... CON COPY_ONLY...  
  
###  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usar PowerShell  
  
Utilice el cmdlet `Backup-SqlDatabase` con el parámetro `-CopyOnly`.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  

### <a name="to-create-a-full-or-log-backup"></a>Para crear una copia de seguridad completa o de registros
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
### <a name="to-view-copy-only-backups"></a>Para ver copias de seguridad de solo copia
  
-   [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
### <a name="to-set-up-and-use-the-sql-server-powershell-provider"></a>Para configurar y usar el proveedor de SQL Server PowerShell
  
-   [Proveedor de SQL Server PowerShell Provider](../../powershell/sql-server-powershell-provider.md)  

## <a name="see-also"></a>Consulte también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [Copiar bases de datos con copias de seguridad y restauración](../databases/copy-databases-with-backup-and-restore.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
