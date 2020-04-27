---
title: Restauraciones de archivos (modelo de recuperación completa) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- full recovery model [SQL Server], performing restores
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- file restores [SQL Server], full recovery model
- restoring files [SQL Server], full recovery model
- Transact-SQL restore sequence
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: d2236a2a-4cf1-4c3f-b542-f73f6096e15c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a78b177b1fb429535a4bb9b271d0b1dbc4eedc79
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62921946"
---
# <a name="file-restores-full-recovery-model"></a>Restauraciones de archivos (modelo de recuperación completa)
  Este tema solo es pertinente para las bases de datos que contienen varios archivos o grupos de archivos con el modelo de recuperación completa o de carga masiva.  
  
 El objetivo de una restauración de archivos consiste en restaurar uno o varios archivos dañados sin necesidad de restaurar la totalidad de la base de datos. Un escenario de restauración de archivos consiste en una única secuencia de restauración que copia, pone al día y recupera los datos apropiados.  
  
 Si el grupo de archivos que se restaura es de lectura/escritura, es necesario aplicar una cadena ininterrumpida de copias de seguridad de registros después de que se restaure la última copia de seguridad de datos o diferencial. De esta forma, el grupo de archivos se actualiza a los registros existentes en los registros activos actuales del archivo de registro. Normalmente, el punto de recuperación está cerca del final del registro, aunque no necesariamente.  
  
 Si el grupo de archivos que se restaura es de solo lectura, por lo general, la aplicación de las copias de seguridad de registros no es necesaria y se omitirá. Si se hizo la copia de seguridad después de que el archivo pasará a ser de solo lectura, será la última copia de seguridad que se restaurará. La puesta al día se detiene en el punto de destino.  
  
 Los escenarios de restauración de archivos son los siguientes:  
  
-   Restauración de archivos sin conexión  
  
     En una *restauración de archivos sin conexión*, la base de datos permanece sin conexión mientras se restauran los archivos o grupos de archivos dañados. Al final de la secuencia de restauración, la base de datos pasará a estar en línea.  
  
     Todas las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admiten restauraciones de archivos sin conexión.  
  
-   Restauración de archivos en línea  
  
     En *restauración de archivos en línea*, si la base de datos está en línea durante una restauración de archivos, permanecerá en línea durante la restauración de archivos. Sin embargo, cada grupo de archivos en el que se restaura un archivo está sin conexión durante la operación de restauración. Una vez recuperados todos los archivos de un grupo de archivos sin conexión, este se conecta automáticamente.  
  
     Para más información sobre la restauración con conexión de archivos y páginas, vea [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Para obtener más información sobre la restauración con conexión, vea [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md).  
  
    > [!TIP]  
    >  Si quiere que la base de datos esté sin conexión durante una restauración de archivos, deje sin conexión la base de datos de que empiece a restaurar la secuencia realizando la acción siguiente [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) : ALTER DATABASE *nombre_base_de_datos* SET OFFLINE.  
  
  
  
##  <a name="restoring-damaged-files-from-file-backups"></a><a name="Overview"></a> Restaurar archivos dañados a partir de copias de seguridad de archivo  
  
1.  Antes de restaurar uno o varios archivos dañados, intente crear una [copia del final del registro](tail-log-backups-sql-server.md).  
  
     Si se ha dañado el registro, no se puede crear una copia del final del registro y se debe restaurar toda la base de datos.  
  
     Para obtener más información sobre cómo hacer una copia de seguridad de un registro de transacciones, vea [Copias de seguridad del registro de transacciones &#40;SQL Server&#41;](transaction-log-backups-sql-server.md).  
  
    > [!IMPORTANT]  
    >  En restauraciones de archivos sin conexión, siempre debe realizar una copia del final de registros después del error antes de la restauración de archivos. En restauraciones de archivos en línea, siempre debe realizar la copia de seguridad de registros después de la restauración de archivos. Esta copia de seguridad de registros es necesaria para que el archivo pueda recuperarse a un estado coherente con el resto de la base de datos.  
  
2.  Restaure cada archivo dañado a partir de la copia de seguridad más reciente de ese archivo.  
  
3.  Restaure la copia de seguridad diferencial de archivos más reciente, si existe, para cada archivo restaurado.  
  
4.  Restaure las copias de seguridad del registro de transacciones en orden, comenzando con la copia de seguridad que abarca el más antiguo de los archivos restaurados y finalizando con la copia del final del registro después del error creada en el paso 1.  
  
     Debe hacer que la base de datos sea coherente; para ello, restaure las copias de seguridad del registro de transacciones creadas después de las copias de seguridad de archivos. Las copias de seguridad del registro de transacciones se pueden poner al día rápidamente, porque solo se aplican los cambios correspondientes a los archivos restaurados. La restauración de archivos individuales puede ser mejor que la restauración de toda la base de datos, dado que los archivos dañados no se copian y, posteriormente, ponen al día. Sin embargo, aún debe leerse toda la cadena de copias de seguridad de registros.  
  
5.  Recupere la base de datos.  
  
> [!NOTE]  
>  Las copias de seguridad de archivos se pueden utilizar para restaurar la base de datos a un momento anterior. Para ello, debe restaurar un conjunto completo de copias de seguridad de archivos y, a continuación, restaurar las copias de seguridad del registro de transacciones en orden hasta llegar al momento específico establecido, que es después del final de la copia de seguridad de archivos restaurada más reciente. Para obtener más información sobre la recuperación a un momento dado, vea [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>Secuencia de restauración de Transact-SQL para la restauración de archivos sin conexión (modelo de recuperación completa)  
 Un escenario de restauración de archivos consiste en una única secuencia de restauración que copia, pone al día y recupera los datos apropiados.  
  
 En esta sección se muestran las opciones esenciales de [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) para una secuencia de restauración de archivos. La sintaxis y los detalles no pertinentes para este propósito se omiten.  
  
 La secuencia de restauración de ejemplo siguiente muestra una restauración sin conexión de dos archivos secundarios, `A` y `B`, mediante WITH NORECOVERY. A continuación, se aplican dos copias de seguridad de registros con NORECOVERY y, después, la copia del final del registro después del error, recuperada con WITH RECOVERY.  
  
> [!NOTE]  
>  El siguiente ejemplo de secuencia de restauración se inicia tomando el archivo sin conexión y después crea una copia del final del registro.  
  
```  
--Take the file offline.  
ALTER DATABASE database_name MODIFY FILE SET OFFLINE;  
-- Back up the currently active transaction log.  
BACKUP LOG database_name  
   TO <tail_log_backup>  
   WITH NORECOVERY;  
GO   
-- Restore the files.  
RESTORE DATABASE database_name FILE=name   
   FROM <file_backup_of_file_A>   
   WITH NORECOVERY;  
RESTORE DATABASE database_name FILE=<name> ......  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
-- Restore the log backups.  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <tail_log_backup>   
   WITH RECOVERY;  
```  
  
## <a name="examples"></a>Ejemplos  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración sin conexión del grupo de archivo principal y de otro grupo de archivos &#40;modelo de recuperación completa&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
 **Para restaurar archivos y grupos de archivos**  
  
-   [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
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
  
  
