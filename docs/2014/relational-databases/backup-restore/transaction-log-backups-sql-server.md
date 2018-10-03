---
title: Copias de seguridad de registros de transacciones (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server[
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6dc94409e607c91944a2263ac5dfb3e8a3f4ce54
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168645"
---
# <a name="transaction-log-backups-sql-server"></a>Copias de seguridad de registros de transacciones (SQL Server)
  Este tema solamente es aplicable a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el modelo de recuperación optimizado para cargas masivas de registros o el modelo de recuperación completa. En este tema se describe cómo se realizan copias de seguridad del registro de transacciones de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Como mínimo, debe haber creado al menos una copia de seguridad completa antes de poder generar una copia de seguridad de registros. A continuación, la copia de seguridad del registro de transacciones se podrá crear en cualquier momento, a menos que ya se haya realizado previamente. Se recomienda realizar copias de seguridad de registros con frecuencia para minimizar el riesgo de pérdida de trabajo y el truncamiento del registro de transacciones. Normalmente, un administrador de bases de datos crea una copia de seguridad completa de la base de datos, por ejemplo, semanalmente; si lo desea, también puede crear una serie de copias de seguridad diferenciales de la base de datos a intervalos más cortos, por ejemplo, a diario. Con independencia de las copias de seguridad de la base de datos, el administrador de la base de datos hace copias de seguridad del registro de transacciones cada poco tiempo, por ejemplo, cada 10 minutos. En el caso de un tipo de copia de seguridad concreto, el intervalo óptimo dependerá de diversos factores, como la importancia de los datos, el tamaño de la base de datos y la carga de trabajo del servidor.  
  
 **En este tema:**  
  
-   [Cómo funciona una secuencia de copias de seguridad del registro](#LogBackupSequence)  
  
-   [Recomendaciones](#Recommendations)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="LogBackupSequence"></a> Cómo funciona una secuencia de copias de seguridad del registro  
 La secuencia de las copias de seguridad del registro de transacciones ( *cadena de registros* ) es independiente de las copias de seguridad de los datos. Por ejemplo, suponga la siguiente secuencia de eventos.  
  
|Time|Evento|  
|----------|-----------|  
|8:00 a. m.|Copia de seguridad de la base de datos.|  
|Mediodía|Copia de seguridad del registro de transacciones.|  
|4:00 p. m.|Copia de seguridad del registro de transacciones.|  
|6:00 p. m.|Copia de seguridad de la base de datos.|  
|8:00 p. m.|Copia de seguridad del registro de transacciones.|  
  
 La copia de seguridad de registros de transacciones creada a las 8:00 p.m contiene las entradas de registros de transacciones comprendidas entre las 4:00 p.m. y las 8:00 p.m., período que abarca el momento en que se creó la copia de seguridad de base de datos completa (a las 6:00 p.m.). La secuencia de copias de seguridad de registros de transacciones es continua desde la primera copia de seguridad de base de datos completa, creada a las 8:00 a.m. hasta la última copia de seguridad de registros de transacciones, creada a las 8:00 p.m. Para obtener más información sobre cómo aplicar estas copias de seguridad de registros, vea el ejemplo de [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
##  <a name="Recommendations"></a> Recomendaciones  
  
-   Si el registro de transacciones resulta dañado, perderá el trabajo realizado desde la última copia de seguridad válida. Por tanto, le recomendamos encarecidamente que sitúe los archivos de registro en un almacenamiento con tolerancia a errores.  
  
-   Si una base de datos se daña o se va a restaurar, se recomienda crear una [copia del final del registro](tail-log-backups-sql-server.md) para que pueda restaurar la base de datos hasta el momento actual.  
  
-   De forma predeterminada, cada operación de copia de seguridad correcta agrega una entrada en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos del sistema. Si hace una copia de seguridad del registro de transacciones con frecuencia, estos mensajes que indican la corrección de la operación pueden acumularse rápidamente, con lo que se crean registros de errores muy grandes que pueden dificultar la búsqueda de otros mensajes. En esos casos, puede suprimir estas entradas de registro utilizando la marca de seguimiento 3226 si ninguno de los scripts depende de esas entradas. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para crear una copia de seguridad del registro de transacciones**  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 Para programar trabajos de copia de seguridad, vea [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md).  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
 Ninguno.  
  
## <a name="see-also"></a>Vea también  
 [El registro de transacciones &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Copias del final del registro &#40;SQL Server&#41;](tail-log-backups-sql-server.md)   
 [Aplicar copias de seguridad de registros de transacción &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
