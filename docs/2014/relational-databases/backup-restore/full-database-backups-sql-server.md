---
title: Copias de seguridad completas de bases de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- backups [SQL Server], database
- backing up databases [SQL Server], full backups
- estimating database backup size
- backing up [SQL Server], size of backup
- database backups [SQL Server], full backups
- size [SQL Server], backups
- database backups [SQL Server], about backing up databases
ms.assetid: 4d933d19-8d21-4aa1-8153-d230cb3a3f99
caps.latest.revision: 62
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4f38f25c58b52b4535e0a91831d1d3de48ccff82
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217495"
---
# <a name="full-database-backups-sql-server"></a>Copias de seguridad completas de bases de datos (SQL Server)
  Una copia de seguridad completa de la base de datos crea una copia de seguridad de toda la base de datos, Esto incluye la parte del registro de transacciones para poder recuperar la base de datos completa después de restaurar una copia de seguridad completa de la base de datos. Las copias de seguridad completas representan la base de datos en el momento en que finalizó la copia de seguridad.  
  
> [!TIP]  
>  A medida que la base de datos aumenta de tamaño, las copias de seguridad completas requieren una mayor cantidad de tiempo para finalizar y espacio de almacenamiento. Por ello, para una base de datos grande, puede que desee complementar una copia de seguridad completa con una serie de *copias de seguridad diferenciales*. Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md).  
  
> [!IMPORTANT]  
>  TRUSTWORTHY se establece en OFF en una copia de seguridad de base de datos. Para obtener información sobre cómo establecer TRUSTWORTHY en ON, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 **En este tema:**  
  
-   [Copias de seguridad de la base de datos en el modelo de recuperación simple](#DbBuRMs)  
  
-   [Copias de seguridad de la base de datos en el modelo de recuperación completa](#DbBuRMf)  
  
-   [Usar una copia de seguridad completa de la base de datos para restaurar la base de datos](#RestoreDbBu)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="DbBuRMs"></a> Copias de seguridad de la base de datos en el modelo de recuperación simple  
 Con el modelo de recuperación simple, después de cada copia de seguridad, la base de datos queda expuesta a la pérdida potencial del trabajo en caso de desastre. El riesgo de pérdida del trabajo se incrementa con cada actualización hasta la siguiente copia de seguridad, cuando el riesgo de pérdida vuelve a cero y empieza un nuevo ciclo de riesgo. El riesgo de pérdida de trabajo aumenta con el tiempo entre una copia de seguridad y otra. La siguiente ilustración muestra el riesgo de pérdida del trabajo en una estrategia de copia de seguridad que solo usa copias de seguridad completas de la base de datos.  
  
 ![Muestra el riesgo de pérdida de trabajo entre copias de seguridad de bases de datos](../../database-engine/media/bnr-rmsimple-1-fulldb-backups.gif "Muestra el riesgo de pérdida de trabajo entre copias de seguridad de bases de datos")  
  
### <a name="example-includetsqlincludestsql-mdmd"></a>Ejemplo ([!INCLUDE[tsql](../../../includes/tsql-md.md)])  
 El siguiente ejemplo muestra cómo crear una copia de seguridad completa de la base de datos mediante WITH FORMAT para sobrescribir cualquier copia de seguridad existente y crear un nuevo conjunto de medios.  
  
```  
-- Back up the AdventureWorks2012 database to new media set.  
BACKUP DATABASE AdventureWorks2012  
    TO DISK = 'Z:\SQLServerBackups\AdventureWorksSimpleRM.bak'   
    WITH FORMAT;  
GO  
```  
  
##  <a name="DbBuRMf"></a> Copias de seguridad de la base de datos en el modelo de recuperación completa  
 En las bases de datos que usan la recuperación completa y optimizada para cargas masivas de registros, las copias de seguridad de base de datos son necesarias pero no suficientes. También se requieren copias de seguridad de registros de transacciones. La siguiente ilustración muestra la estrategia de copia de seguridad menos compleja en un modelo de recuperación completa.  
  
 ![Serie de copias de seguridad completas de bases de datos y copias de seguridad de registros](../../database-engine/media/bnr-rmfull-1-fulldb-log-backups.gif "Serie de copias de seguridad completas de bases de datos y copias de seguridad de registros")  
  
 Para obtener información sobre cómo crear copias de seguridad de registros, vea [Copias de seguridad de registros de transacciones &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
### <a name="example-includetsqlincludestsql-mdmd"></a>Ejemplo ([!INCLUDE[tsql](../../../includes/tsql-md.md)])  
 El siguiente ejemplo muestra cómo crear una copia de seguridad completa de la base de datos mediante WITH FORMAT para sobrescribir cualquier copia de seguridad existente y crear un nuevo conjunto de medios. A continuación, en el ejemplo se realiza una copia de seguridad del registro de transacciones. En una situación real, deberá realizar una serie de copias de seguridad de registros periódicas. Para este ejemplo, la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] se configura para usar el modelo de recuperación completa.  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
-- Back up the AdventureWorks2012 database to new media set (backup set 1).  
BACKUP DATABASE AdventureWorks2012  
  TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012FullRM.bak'   
  WITH FORMAT;  
GO  
--Create a routine log backup (backup set 2).  
BACKUP LOG AdventureWorks2012 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012FullRM.bak';  
GO  
```  
  
##  <a name="RestoreDbBu"></a> Usar una copia de seguridad completa de la base de datos para restaurar la base de datos  
 Es posible volver a crear toda la base de datos en un único paso; para ello, restaure la base de datos a partir de una copia de seguridad completa. En la copia de seguridad se incluye suficiente información del registro de transacciones como para permitir la recuperación de la base de datos en el punto en que se completó la copia de seguridad. El estado de la base de datos restaurada será el mismo que el de la base de datos original en el momento en que terminó la copia de seguridad de base de datos, menos algunas transacciones no confirmadas. Con el modelo de recuperación completa, debe restaurar todas las copias de seguridad de registros de transacciones siguientes. Una vez recuperada la base de datos, las transacciones no confirmadas se revierten.  
  
 Para obtener más información, vea [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](complete-database-restores-simple-recovery-model.md) o [Restauraciones de base de datos completas &#40;modelo de recuperación completa&#41;](complete-database-restores-full-recovery-model.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para crear una copia de seguridad completa de la base de datos**  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 **Para programar trabajos de copia de seguridad**  
  
 [Usar el Asistente para planes de mantenimiento](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](back-up-and-restore-of-sql-server-databases.md)   
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
