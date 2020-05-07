---
title: Recuperación a un número de secuencia de registro (SQL Server) | Microsoft Docs
description: En SQL Server, puede usar el número de secuencia de registro (LSN) para realizar una recuperación a un momento determinado. Esta característica está destinada a los proveedores de herramientas.
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- log sequence numbers [SQL Server]
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- LSNs
- database recovery [SQL Server]
- database restores [SQL Server], point in time
ms.assetid: f7b3de5b-198d-448d-8c71-1cdd9239676c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a7b5233b44610ce5d2ad15d5a7aceda207f077dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180901"
---
# <a name="recover-to-a-log-sequence-number-sql-server"></a>Recuperar a un número de secuencia de registro (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema solamente es aplicable a las bases de datos que utilizan el modelo de recuperación optimizado para cargas masivas de registros o el modelo de recuperación completa.  
  
 Puede usar un número de secuencia de registro (LSN) para definir el punto de recuperación de una operación de restauración. Sin embargo, esta es una característica especializada dirigida a los proveedores de herramientas y no es probable que tenga una utilidad general.  
  
##  <a name="overview-of-log-sequence-numbers"></a><a name="LSNs"></a> Información general de los números de secuencia de registro  
 Los LSN se utilizan internamente durante una secuencia RESTORE para realizar el seguimiento del momento dado al que se restauran los datos. Al restaurar una copia de seguridad, los datos se restauran al LSN correspondiente al momento dado en que se efectuó la copia de seguridad. Las copias de seguridad diferenciales y del registro posponen la base de datos restaurada a un momento posterior, correspondiente a un LSN superior. Para obtener más información sobre LSN, vea [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch).  
  
> [!NOTE]  
> Los números LSN son valores con tipos de datos **numeric**(25,0). Las operaciones aritméticas (por ejemplo, la suma o la resta) carecen de importancia y no deben utilizarse con los LSN.  
 
## <a name="viewing-lsns-used-by-backup-and-restore"></a>Visualización de LSN utilizados por las copias de seguridad y restauración  
 El LSN de una entrada de registro en la que se produce un determinado evento de copias de seguridad y restauración puede visualizarse mediante uno o más de los siguientes métodos:  
  
-   [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
-   [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
  
-   [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md); [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
-   [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
-   [RESTORE FILELISTONLY](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
> [!NOTE]  
>  Los LSN también aparecen en algunos mensajes en el registro de errores.  
  
## <a name="transact-sql-syntax-for-restoring-to-an-lsn"></a>Sintaxis de Transact-SQL para restaurar hasta un LSN  
 Con la instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) , puede detenerse en el LSN o inmediatamente antes, como se indica a continuación:  
  
-   Use la cláusula WITH STOPATMARK **='** lsn: _<númeroDeIsn>_ **'** , donde lsn: *\<númeroDeIsn>* es una cadena que especifica que la entrada de registro que contiene el LSN especificado es el punto de recuperación.  
  
     STOPATMARK realiza una puesta al día hasta el LSN e incluye esa entrada de registro en la puesta al día.  
  
-   Use la cláusula WITH STOPBEFOREMARK **='** lsn: _<númeroDeIsn>_ **'** , donde lsn: *\<númeroDeIsn>* es una cadena que especifica que la entrada de registro inmediatamente anterior a la entrada que contiene el número LSN especificado es el punto de recuperación.  
  
     STOPBEFOREMARK realiza una puesta al día al LSN y excluye esa entrada de registro de la puesta al día.  
  
 Normalmente, se selecciona una transacción específica para incluirla o excluirla. Aunque no es necesario, en la práctica, la entrada de registro especificada es una entrada de confirmación de transacción.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se da por supuesto que se ha modificado la base de datos `AdventureWorks` para usar el modelo de recuperación completa.  
  
```sql  
RESTORE LOG AdventureWorks FROM DISK = 'c:\adventureworks_log.bak'   
WITH STOPATMARK = 'lsn:15000000040000037'  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar una base de datos según el punto de error en el modelo de recuperación completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar una base de datos en una transacción marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
## <a name="see-also"></a>Consulte también  
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [Información general sobre restauración y recuperación (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)       
 [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)      
  
