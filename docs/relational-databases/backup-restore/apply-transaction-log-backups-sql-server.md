---
title: Aplicar copias de seguridad de registros de transacción (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 62d90931cdc1d7748f47edabb31e5f9404b1262d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72916199"
---
# <a name="apply-transaction-log-backups-sql-server"></a>Aplicar copias de seguridad de registros de transacción (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema solo es relevante para el modelo de recuperación completa o para el modelo de recuperación optimizado para cargas masivas de registros.  
  
 En este tema se describe la aplicación de copias de seguridad del registro de transacciones como parte de la restauración de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
##  <a name="Requirements"></a> Requisitos para restaurar las copias de seguridad del registro de transacciones  
 Para aplicar una copia de seguridad del registro de transacciones, deben cumplirse los requisitos siguientes:  
  
-   **Suficientes copias de seguridad de registros para una secuencia de restauración:** debe tener suficientes copias de seguridad de entradas de registro para poder completar una secuencia de restauración. Las copias de seguridad de registros necesarias, incluida la [copia del final del registro](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) si es necesaria, deben estar disponibles antes de iniciar la secuencia de restauración.  
  
-   **Orden de restauración correcto**  : primero debe restaurarse la copia de seguridad diferencial de la base de datos o la copia de seguridad completa inmediatamente anterior de la base de datos. A continuación, todos los registros de transacciones creados después de esa copia de seguridad completa o diferencial de la base de datos deben restaurarse en orden cronológico. Si se pierde o se daña una copia de seguridad del registro de transacciones en esta cadena de registros, solo puede restaurar los registros de transacciones anteriores al registro de transacciones que falta.  
  
-   **La base de datos no se ha recuperado todavía:**  no se puede recuperar la base de datos hasta que se haya aplicado el registro de transacciones final. Si recupera la base de datos después de restaurar una de las copias de seguridad intermedias del registro de transacciones, anterior al final de la cadena de registros, no podrá restaurar la base de datos más allá de ese punto sin reiniciar toda la secuencia de restauración, empezando por la copia de seguridad completa de la base de datos.  
  
    > [!TIP]
    > Es aconsejable restaurar todas las copias de seguridad de registros (`RESTORE LOG *database_name* WITH NORECOVERY`). A continuación, después de restaurar la última copia de seguridad de registros, recupere la base de datos en una operación aparte (`RESTORE DATABASE *database_name* WITH RECOVERY`).  
  
##  <a name="RecoveryAndTlogs"></a> Registros de transacciones y recuperación  
 Cuando finalice la operación de restauración y recupere la base de datos, se ejecutará el proceso de recuperación para garantizar la integridad de la base de datos. Para más información sobre el proceso de recuperación, vea [Información general sobre restauración y recuperación (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery).
 
 Después de que se complete el proceso de recuperación, la base de datos pasa a estar en línea y no se pueden aplicar más copias de seguridad del registro de transacciones a la base de datos. Por ejemplo, una serie de copias de seguridad del registro de transacciones contiene una transacción de larga duración. El inicio de la transacción se registra en la primera copia de seguridad del registro de transacciones, pero el final de la transacción se registra en la segunda copia de seguridad. En la primera copia de seguridad del registro de transacciones no se registra ninguna operación de confirmación o reversión. Si se ejecuta una operación de recuperación cuando se aplica la primera copia de seguridad del registro de transacciones, la transacción de larga ejecución se trata como incompleta y se revierten las modificaciones de datos registradas en la primera copia de seguridad del registro de transacciones de la transacción. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite la aplicación de la segunda copia de seguridad del registro de transacciones a partir de este punto.  
  
> [!NOTE]
> En algunas circunstancias, es posible agregar un archivo explícitamente durante la restauración del registro.  
  
##  <a name="PITrestore"></a> Usar copias de seguridad de registros para restaurar hasta el momento del error  
 Suponga el siguiente flujo de eventos.  
  
|Time|Evento|  
|----------|-----------|  
|8:00 a. m.|Copia de seguridad de la base de datos para crear una copia de seguridad completa de la base de datos.|  
|Mediodía|Copia de seguridad del registro de transacciones.|  
|4:00 p. m.|Copia de seguridad del registro de transacciones.|  
|6:00 p. m.|Copia de seguridad de la base de datos para crear una copia de seguridad completa de la base de datos.|  
|8:00 p. m.|Copia de seguridad del registro de transacciones.|  
|9:45 p. m.|Se produce el error.|  
  
> Para obtener una explicación de este ejemplo de secuencia de copias de seguridad, vea [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
 Para restaurar la base de datos a su estado a las 21:45 (el punto de error), se puede utilizar cualquiera de los siguientes procedimientos:  

 **Alternativa 1: restaurar la base de datos mediante la copia de seguridad completa de la base de datos más reciente**  
  
1.  Cree una copia del final del registro de transacciones activo actualmente como si fuera el del momento del error.  
  
2.  No restaure la copia de seguridad completa de base de datos de las 6:00 p. m. En su lugar, restaure la copia de seguridad completa de la base de datos de las 6:00 p.m. más reciente y, a continuación, aplique la copia de seguridad de registros y la copia del final del registro de las 8:00 p. m.  
  
 **Alternativa 2: restaurar la base de datos mediante una copia de seguridad completa de la base de datos anterior**  
  
> Este proceso alternativo resulta útil si un problema impide que se use la copia de seguridad completa de base de datos de las 6:00 p. m. Este proceso lleva más tiempo que restaurar a partir de la copia de seguridad completa de base de datos de las 6:00 p. m.  
  
1.  Cree una copia del final del registro de transacciones activo actualmente como si fuera el del momento del error.  
  
2.  Restaure la copia de seguridad completa de base de datos de las 8:00 a.m. y, a continuación, restaure secuencialmente las cuatro copias de seguridad del registro de transacciones. Esta acción pone al día todas las transacciones completadas hasta las 9:45 p. m.  
  
     Esta alternativa señala la seguridad redundante que ofrece el mantenimiento de una cadena de copias de seguridad del registro de transacciones a través de una serie de copias de seguridad completas de base de datos.  
  
> En algunos casos, también se pueden utilizar registros de transacciones para restaurar una base de datos hasta un momento específico. Para obtener más información, vea [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
##  <a name="RelatedTasks"></a> Related tasks  
 **Para aplicar una copia de seguridad del registro de transacciones**  
  
-   [Restaurar una copia de seguridad de registros de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
 **Para restaurar hasta su punto de recuperación**  
  
-   [Restaurar una base de datos según el punto de error en el modelo de recuperación completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [Recuperación de bases de datos relacionadas que contienen transacciones marcadas](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [Recuperar a un número de secuencia de registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
 **Para recuperar una base de datos después de restaurar las copias de seguridad mediante WITH NORECOVERY**  
  
-   [Recuperar una base de datos sin restaurar los datos &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)      
  
