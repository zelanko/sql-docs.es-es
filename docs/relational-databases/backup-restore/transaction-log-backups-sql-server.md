---
title: Copias de seguridad de registros de transacciones (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 491016d02dfdb890914633333e19a3138c01779d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68041353"
---
# <a name="transaction-log-backups-sql-server"></a>Copias de seguridad de registros de transacciones (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema solamente es aplicable a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el modelo de recuperación optimizado para cargas masivas de registros o el modelo de recuperación completa. En este tema se describe cómo se realizan copias de seguridad del registro de transacciones de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Como mínimo, debe haber creado al menos una copia de seguridad completa antes de poder generar una copia de seguridad de registros. A continuación, la copia de seguridad del registro de transacciones se podrá crear en cualquier momento, a menos que ya se haya realizado previamente. 
 
Se recomienda realizar copias de seguridad de registros con frecuencia para minimizar el riesgo de pérdida de trabajo y el truncamiento del registro de transacciones. 
 
Un administrador de bases de datos normalmente crea una copia de seguridad completa de la base de datos, por ejemplo, semanalmente; si lo desea, también puede crear una serie de copias de seguridad diferenciales de la base de datos a intervalos más cortos, por ejemplo, a diario. Con independencia de las copias de seguridad de la base de datos, el administrador de la base de datos hace copias de seguridad del registro de transacciones cada poco tiempo. En el caso de un tipo de copia de seguridad concreto, el intervalo óptimo dependerá de diversos factores, como la importancia de los datos, el tamaño de la base de datos y la carga de trabajo del servidor. Para obtener más información sobre cómo implementar una buena estrategia, vea [Recomendaciones](#Recommendations) en este tema. 
   
##  <a name="LogBackupSequence"></a> Cómo funciona una secuencia de copias de seguridad de registros  
 La secuencia de las copias de seguridad del registro de transacciones ( *cadena de registros* ) es independiente de las copias de seguridad de los datos. Por ejemplo, suponga la siguiente secuencia de eventos.  
  
|Time|Evento|  
|----------|-----------|  
|8:00|Copia de seguridad de la base de datos.|  
|Mediodía|Copia de seguridad del registro de transacciones.|  
|16:00|Copia de seguridad del registro de transacciones.|  
|18:00|Copia de seguridad de la base de datos.|  
|20:00|Copia de seguridad del registro de transacciones.|  
  
 La copia de seguridad del registro de transacciones creada a las 20:00 contiene las entradas del registro de transacciones comprendidas entre las 16:00 y las 20:00, período que abarca el momento en que se creó la copia de seguridad de base de datos completa (a las 18:00). La secuencia de copias de seguridad del registro de transacciones es continua, desde la primera copia de seguridad de base de datos completa, creada a las 8:00, hasta la última copia de seguridad del registro de transacciones, creada a las 20:00. Para obtener más información sobre cómo aplicar estas copias de seguridad de registros, vea el ejemplo de [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
##  <a name="Recommendations"></a> Recomendaciones  
  
-   Si el registro de transacciones resulta dañado, perderá el trabajo realizado desde la última copia de seguridad válida. Por tanto, le recomendamos encarecidamente que sitúe los archivos de registro en un almacenamiento con tolerancia a errores.  
  
-   Si una base de datos se daña o se va a restaurar, se recomienda crear una [copia del final del registro](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) para que pueda restaurar la base de datos hasta el momento actual.  
  
-   De forma predeterminada, cada operación de copia de seguridad correcta agrega una entrada en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos del sistema. Si hace una copia de seguridad del registro de transacciones con frecuencia, estos mensajes que indican la corrección de la operación pueden acumularse rápidamente, con lo que se crean registros de errores muy grandes que pueden dificultar la búsqueda de otros mensajes. En esos casos, puede suprimir estas entradas de registro utilizando la marca de seguimiento 3226 si ninguno de los scripts depende de esas entradas. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  

-   Realice copias de seguridad de registros suficientemente regulares para ajustarse a los requisitos de la empresa, específicamente a la tolerancia a la pérdida de trabajo que un almacenamiento de registro dañado podría provocar. 
   -   La frecuencia adecuada para realizar copias de seguridad de registros varía en función de la tolerancia al riesgo de pérdida de trabajo y, por otra parte, de la cantidad de copias de seguridad de registros que puede almacenar, administrar y, potencialmente, restaurar. Tenga en cuenta los [RTO](https://wikipedia.org/wiki/Recovery_time_objective) y [RPO](https://wikipedia.org/wiki/Recovery_point_objective) necesarios al implementar la estrategia de recuperación, específicamente el ritmo de realización de copias de seguridad de registros.
   -   Una copia de seguridad de registros cada 15 ó 30 minutos puede ser suficiente. Si su empresa necesita minimizar el riesgo de pérdida de trabajo, piense en la posibilidad de realizar copias de seguridad de registros más frecuentemente. La existencia de copias de seguridad más frecuentes de los registros tiene la ventaja añadida de aumentar la frecuencia de truncamiento del registro, lo que genera archivos de registro menores.  
  
> [!IMPORTANT]
> Para limitar el número de copias de seguridad del registro que necesita restaurar, es esencial que realice una copia de seguridad de sus datos periódicamente. Por ejemplo, podría programar una copia de seguridad completa de la base de datos cada semana y copias de seguridad diferenciales de la base de datos a diario.  
> Una vez más, tenga en cuenta los [RTO](https://wikipedia.org/wiki/Recovery_time_objective) y [RPO](https://wikipedia.org/wiki/Recovery_point_objective) necesarios al implementar la estrategia de recuperación, específicamente el ritmo de realización de copias de seguridad de base de datos completas y diferenciales.
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para crear una copia de seguridad del registro de transacciones**  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 Para programar trabajos de copia de seguridad, vea [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  

## <a name="see-also"></a>Consulte también  
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Copias de seguridad de registros de transacciones en Guía de arquitectura y administración de registros de transacciones de SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [Aplicar copias de seguridad de registros de transacción &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
