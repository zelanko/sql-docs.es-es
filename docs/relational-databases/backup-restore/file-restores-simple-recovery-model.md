---
title: "Restauraciones de archivos (modelo de recuperación simple) | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- file restores [SQL Server]
- simple recovery model [SQL Server]
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- Transact-SQL restore sequence
- restoring files [SQL Server], simple recovery model
- file restores [SQL Server], simple recovery model
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 306ad5cc252c5ba99704f649e24530c3d699de4c
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="file-restores-simple-recovery-model"></a>Restauraciones de archivos (modelo de recuperación simple)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema solo es relevante para las bases de datos de modelo simple que incluyen como mínimo un grupo de archivos secundario de solo lectura.  
  
 El objetivo de una restauración de archivos consiste en restaurar uno o varios archivos dañados sin necesidad de restaurar la totalidad de la base de datos. En el modelo de recuperación simple, las copias de seguridad de archivos se admiten únicamente para los archivos de solo lectura. El grupo de archivos primario y los grupos de archivos secundarios de lectura/escritura se restauran siempre juntos, mediante la restauración de una base de datos o de una copia de seguridad parcial.  
  
 Los escenarios de restauración de archivos son los siguientes:  
  
-   Restauración de archivos sin conexión  
  
     En una *restauración de archivos sin conexión*, la base de datos permanece sin conexión mientras se restauran los archivos o grupos de archivos dañados. Al final de la secuencia de restauración, la base de datos pasará a estar en línea.  
  
     Todas las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admiten restauraciones de archivos sin conexión.  
  
-   Restauración de archivos en línea  
  
     En *restauración de archivos en línea*, si la base de datos está en línea durante una restauración de archivos, permanecerá en línea durante la restauración de archivos. Sin embargo, cada grupo de archivos en el que se restaura un archivo está sin conexión durante la operación de restauración. Una vez recuperados todos los archivos de un grupo de archivos sin conexión, este se conecta automáticamente.  
  
     Para información sobre la compatibilidad con la restauración en línea de la página y de archivo, vea [Características y tareas del motor de base de datos](http://msdn.microsoft.com/library/d9efe145-3306-4d61-bd77-e2af43e19c34). Para obtener más información sobre la restauración con conexión, vea [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Si quiere que la base de datos esté sin conexión durante una restauración de archivos, deje sin conexión la base de datos de que empiece a restaurar la secuencia realizando la acción siguiente [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) : ALTER DATABASE *nombre_base_de_datos* SET OFFLINE.  
  
 **En este tema:**  
  
-   [Información general acerca de la restauración de archivos y grupos de archivos con el modelo de recuperación simple](#Overview)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="Overview"></a> Información general acerca de la restauración de archivos y grupos de archivos con el modelo de recuperación simple  
 Un escenario de restauración de archivos está formado por una única secuencia de restauración que copia, pone al día y recupera los datos apropiados de la siguiente manera:  
  
1.  Restaure cada archivo dañado a partir de su copia de seguridad de archivo más reciente.  
  
2.  Restaure la copia de seguridad diferencial de archivos más reciente para cada archivo restaurado y recupere la base de datos.  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>Secuencia de restauración de Transact-SQL para la restauración de archivos (modelo de recuperación simple)  
 Esta sección muestra las opciones fundamentales de [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] de una secuencia de restauración de archivos simple. La sintaxis y los detalles no pertinentes para este propósito se omiten.  
  
 La secuencia de restauración solo contiene dos instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La primera instrucción restaura un archivo secundario, el archivo `A`, que se restaura usando WITH NORECOVERY. La segunda operación restaura otros dos archivos, `B` y `C` , que se restauran usando WITH RECOVERY desde un dispositivo de copia de seguridad diferente:  
  
1.  RESTORE DATABASE *base_de_datos* FILE **=***nombre_de_archivo_A*  
  
     FROM *copia_de_seguridad_de_archivo_A*  
  
     WITH NORECOVERY**;**  
  
2.  RESTORE DATABASE *base_de_datos* FILE **=***nombre_de_archivo_B***,***nombre_de_archivo_C*  
  
     FROM *copia_de_seguridad_de_archivos_B_y_C*  
  
     WITH RECOVERY**;**  
  
### <a name="examples"></a>Ejemplos  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración sin conexión del grupo de archivo principal y de otro grupo de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para restaurar archivos y grupos de archivos**  
  
-   [Restaurar archivos y grupos de archivos en archivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Método Restore.SqlRestore (servidor) (SMO)](http://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.restore.sqlrestore.aspx)   
  
## <a name="see-also"></a>Ver también  
 [Copias de seguridad y restauración: interoperabilidad y coexistencia &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Copias de seguridad diferenciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Copias de seguridad de archivos completas &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
