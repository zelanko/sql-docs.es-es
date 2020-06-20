---
title: Restauraciones de archivos (modelo de recuperación simple) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2ed48f48f531e727de5d6e1403ef47f5399f874d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958071"
---
# <a name="file-restores-simple-recovery-model"></a>Restauraciones de archivos (modelo de recuperación simple)
  Este tema solo es relevante para las bases de datos de modelo simple que incluyen como mínimo un grupo de archivos secundario de solo lectura.  
  
 El objetivo de una restauración de archivos consiste en restaurar uno o varios archivos dañados sin necesidad de restaurar la totalidad de la base de datos. En el modelo de recuperación simple, las copias de seguridad de archivos se admiten únicamente para los archivos de solo lectura. El grupo de archivos primario y los grupos de archivos secundarios de lectura/escritura se restauran siempre juntos, mediante la restauración de una base de datos o de una copia de seguridad parcial.  
  
 Los escenarios de restauración de archivos son los siguientes:  
  
-   Restauración de archivos sin conexión  
  
     En una *restauración de archivos sin conexión*, la base de datos permanece sin conexión mientras se restauran los archivos o grupos de archivos dañados. Al final de la secuencia de restauración, la base de datos pasará a estar en línea.  
  
     Todas las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admiten restauraciones de archivos sin conexión.  
  
-   Restauración de archivos en línea  
  
     En *restauración de archivos en línea*, si la base de datos está en línea durante una restauración de archivos, permanecerá en línea durante la restauración de archivos. Sin embargo, cada grupo de archivos en el que se restaura un archivo está sin conexión durante la operación de restauración. Una vez recuperados todos los archivos de un grupo de archivos sin conexión, este se conecta automáticamente.  
  
     Para más información sobre la restauración con conexión de archivos y páginas, vea [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Para obtener más información sobre la restauración con conexión, vea [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Si quiere que la base de datos esté sin conexión durante una restauración de archivos, deje sin conexión la base de datos antes de iniciar la secuencia de restauración mediante la ejecución de la instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) siguiente: ALTER DATABASE *nombre_base_de_datos* SET OFFLINE.  
  

  
##  <a name="overview-of-file-and-filegroup-restore-under-the-simple-recovery-model"></a><a name="Overview"></a> Información general acerca de la restauración de archivos y grupos de archivos con el modelo de recuperación simple  
 Un escenario de restauración de archivos está formado por una única secuencia de restauración que copia, pone al día y recupera los datos apropiados de la siguiente manera:  
  
1.  Restaure cada archivo dañado a partir de su copia de seguridad de archivo más reciente.  
  
2.  Restaure la copia de seguridad diferencial de archivos más reciente para cada archivo restaurado y recupere la base de datos.  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>Secuencia de restauración de Transact-SQL para la restauración de archivos (modelo de recuperación simple)  
 Esta sección muestra las opciones fundamentales de [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) de [!INCLUDE[tsql](../../../includes/tsql-md.md)] de una secuencia de restauración de archivos simple. La sintaxis y los detalles no pertinentes para este propósito se omiten.  
  
 La secuencia de restauración solo contiene dos instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)] . La primera instrucción restaura un archivo secundario, el archivo `A`, que se restaura usando WITH NORECOVERY. La segunda operación restaura otros dos archivos, `B` y `C` , que se restauran usando WITH RECOVERY desde un dispositivo de copia de seguridad diferente:  
  
1.  RESTORE DATABASE *base_de_datos* FILE **=** _nombre_de_archivo_A_  
  
     FROM *copia_de_seguridad_de_archivo_A*  
  
     WITH NORECOVERY **;**  
  
2.  RESTORE DATABASE *base_de_datos* FILE **=** _nombre_de_archivo_B_ **,** _nombre_de_archivo_C_  
  
     FROM *copia_de_seguridad_de_archivos_B_y_C*  
  
     WITH RECOVERY **;**  
  
### <a name="examples"></a>Ejemplos  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración sin conexión del grupo de archivos principal y de otro grupo de archivos &#40;modelo de recuperación completa&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
 
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
 **Para restaurar archivos y grupos de archivos**  
  
-   [Restaurar archivos y grupos de archivos en archivos existentes &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
  
## <a name="see-also"></a>Consulte también  
 [Copias de seguridad y restauración: interoperabilidad y coexistencia &#40;SQL Server&#41;](backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [Copias de seguridad diferenciales &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [Copias de seguridad de archivos completas &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [Información general de copia de seguridad &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](complete-database-restores-simple-recovery-model.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
