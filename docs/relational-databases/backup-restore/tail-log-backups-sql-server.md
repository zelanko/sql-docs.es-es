---
title: Copias del final del registro (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], tail of log
- transaction log backups [SQL Server], tail-log backups
- NO_TRUNCATE clause
- backups [SQL Server], log backups
- tail-log backups
- backups [SQL Server], tail-log backups
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
caps.latest.revision: 55
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 70b11ff22c345737e95e32695cbe187d846cac00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32920010"
---
# <a name="tail-log-backups-sql-server"></a>Copias del final del registro (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema solamente es pertinente para copias de seguridad y restauración de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el modelo de recuperación optimizado para cargas masivas de registros o el modelo de recuperación completa.  
  
 Una *copia del final del registro* captura las entradas del registro de las que todavía no se ha realizado copia de seguridad (el *final del registro*) para evitar la pérdida de trabajo y mantener intacta la cadena de registros. Para poder recuperar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al último momento, debe realizar una copia del final del registro de transacciones. La copia del final del registro será la copia de seguridad de interés en el plan de recuperación de la base de datos.  
  
> **NOTA:** No todos los escenarios de restauración requieren una copia del final del registro. No necesita una copia del final del registro si el punto de recuperación está incluido en una copia de seguridad de registros anterior. Además, no es necesaria una copia del final del registro si va a mover o reemplazar (sobrescribir) la base de datos y no necesita restaurarla a un momento posterior de la copia de seguridad más reciente.  
  
   ##  <a name="TailLogScenarios"></a> Escenarios que requieren una copia del final del registro  
 Recomendamos realizar una copia del final del registro en los siguientes escenarios:  
  
-   Si la base de datos está en línea y planea realizar una operación de restauración en la base de datos, comience con una copia del final del registro. Para evitar un error para una base de datos en línea, debe utilizar la opción WITH NORECOVERY de la instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Si una base de datos está sin conexión y no puede iniciarse y necesita restaurar la base de datos, primero haga una copia del final del registro. Debido a que no pueden producirse otras transacciones en este momento, el uso de WITH NORECOVERY es opcional.  
  
-   Si se daña una base de datos, intente hacer una copia del final del registro con la opción WITH CONTINUE_AFTER_ERROR de la instrucción BACKUP.  
  
     En una base de datos dañada, la copia del final del registro se puede completar sin errores solo si los archivos de registro no están dañados, si la base de datos tiene un estado que admite copias de seguridad de registros después del error y si la base de datos no contiene cambios registrados de forma masiva. Si no se puede crear una copia del final del registro, se pueden las transacciones confirmadas después de la última copia de seguridad de registros.  
  
 En la tabla siguiente se resumen las opciones BACKUP NORECOVERY y CONTINUE_AFTER_ERROR.  
  
|Opción BACKUP LOG|Comentarios|  
|-----------------------|--------------|  
|NORECOVERY|Use NORECOVERY cada vez que desee continuar con una operación de restauración en la base de datos. NORECOVERY pone la base de datos en el estado de restauración. Esto garantiza que la base de datos no cambie después de realizar la copia del final del registro. El registro se truncará a menos que también se especifique la opción NO_TRUNCATE o COPY_ONLY.<br /><br /> **Importante** Evite usar NO_TRUNCATE, salvo cuando la base de datos esté dañada.|  
|CONTINUE_AFTER_ERROR|Utilice CONTINUE_AFTER_ERROR solo si va a crear una copia del final de una base de datos dañada.<br /><br /> Al realizar una copia de seguridad del final del registro de una base de datos dañada, es posible que parte de los metadatos que comúnmente se capturan en las copias de seguridad de registros no estén disponibles. Para más información, consulte [Copias del final del registro con metadatos de copia de seguridad incompletos](#IncompleteMetadata)que aparece en este tema.|  
  
##  <a name="IncompleteMetadata"></a> Copias del final del registro con metadatos de copia de seguridad incompletos  
 Las copias de seguridad de registros después del error capturan el final del registro aunque falten archivos en la base de datos, o la base de datos esté sin conexión o dañada. Sin embargo, esto puede provocar que se obtengan metadatos incompletos de los comandos de información de restauración y **msdb**. Sin embargo, solo los metadatos están incompletos. El registro capturado está completo y en condiciones de uso.  
  
 Si una copia del final del registro tiene metadatos incompletos, en la tabla [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) se establece **has_incomplete_metadata** en **1**. Asimismo, en la salida de [RESTORE HEADERONLY](../../t-sql/statements/restore-statements-headeronly-transact-sql.md), **HasIncompleteMetadata** se establece en **1**.  
  
 Si los metadatos de la copia del final del registro están incompletos, a la tabla [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md) le faltará la mayoría de la información sobre grupos de archivos en el momento de realizar la copia del final del registro. La mayoría de las columnas de la tabla **backupfilegroup** son NULL; las únicas columnas significativas son las siguientes:  
  
-   **backup_set_id**  
-   **filegroup_id**  
-   **tipo**  
-   **type_desc**  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 Para crear una copia del final del registro, vea [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
 Para restaurar una copia de seguridad del registro de transacciones, vea [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
    
## <a name="see-also"></a>Ver también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Copias de seguridad de solo copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)    
 [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)
  
