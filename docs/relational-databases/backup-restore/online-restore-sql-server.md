---
title: Restauración con conexión (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- online restores [SQL Server]
- online restores [SQL Server], about online restores
ms.assetid: 7982a687-980a-4eb8-8e9f-6894148e7d8c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e4f5817fe575422dddeedd525b077dbf643a29b2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "72908878"
---
# <a name="online-restore-sql-server"></a>Restauración en línea (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La restauración en línea solo se admite en la edición Enterprise de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En esta versión, la restauración de un archivo, una página o por etapas es en línea de manera predeterminada. Este tema es pertinente para las bases de datos que incluyen varios archivos o grupos de archivos y, en el modelo de recuperación simple, solo para grupos de archivos de solo lectura.  
  
 La restauración de datos mientras la base de datos está en línea se denomina *restauración en línea*. Se considera que una base de datos está en línea siempre que el grupo de archivos principal esté en línea, aunque alguno de los grupos de archivos secundarios esté sin conexión. En todos los modelos de recuperación se puede restaurar un archivo sin conexión mientras la base de datos está en línea. En el modelo de recuperación completa, también se pueden restaurar páginas mientras la base de datos está en línea.  
  
> [!NOTE]  
>  La restauración en línea tiene lugar automáticamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise y no requiere ninguna acción por parte del usuario. Si no desea utilizar la restauración en línea, puede dejar una base de datos sin conexión antes de iniciar la restauración. Para obtener más información, vea [Dejar sin conexión una base de datos o un archivo](#taking_db_or_file_offline)más adelante en este tema.  
  
 Durante una operación de restauración de archivos en línea, los archivos que se estén restaurando y su grupo de archivos están sin conexión. Si algunos de dichos archivos está en línea cuando se inicia una restauración en línea, la primera instrucción de la restauración deja sin conexión el grupo de archivos al que pertenece el archivo. Por el contrario, durante una restauración en línea de una página, solo esa página está sin conexión.  
  
 El escenario de restauración en línea implica los siguientes pasos básicos:  
  
1.  Restaure los datos.  
  
2.  Restaure el registro utilizando WITH RECOVERY para la última restauración del registro. Así, se ponen en línea los datos restaurados.  

 A veces, una transacción sin confirmar no se puede revertir porque los datos necesarios para la operación de reversión están sin conexión durante el inicio. En ese caso, la transacción se difiere. Para obtener más información, vea [Transacciones diferidas &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
> [!NOTE]  
>  Si la base de datos está usando en ese momento el modelo de recuperación optimizado para cargas masivas de registros, es recomendable cambiar al modelo de recuperación completa antes de iniciar la restauración en línea. Para obtener más información, vea [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Si las copias de seguridad se realizaron con varios dispositivos conectados al servidor, será necesario que los mismos dispositivos estén disponibles durante una restauración en línea.  
  
> [!CAUTION]  
>  Al utilizar las copias de seguridad de instantánea, no se puede realizar un **Online Restore**. Para obtener más información sobre **Copias de seguridad de instantánea**, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="log-backups-for-online-restore"></a>Copias de seguridad de registros para una restauración en línea  
 En el caso de una restauración en línea, el punto de recuperación es el punto donde se dejaron sin conexión los datos que se van a restaurar o se convirtieron en datos de solo lectura por última vez. Las copias de seguridad del registro de transacciones que llevan a este punto de recuperación y lo incluyen deben estar todas disponibles. Normalmente, es necesario hacer una copia de seguridad de registros después de ese punto para cubrir el punto de recuperación del archivo. La única excepción tiene lugar durante una restauración en línea de datos de solo lectura a partir de una copia de seguridad de datos que se realizó después de que los datos pasaran a ser de solo lectura. En ese caso, no es necesario disponer de una copia de seguridad de registros.  
  
 En general, puede realizar copias de seguridad del registro de transacciones mientras la base de datos esté en línea, incluso después de iniciar la secuencia de restauración. El momento oportuno para la realización de la última copia de seguridad de registros depende de las propiedades del archivo que se va a restaurar:  
  
-   En el caso de un archivo en línea de solo lectura, puede realizar la última copia de seguridad de registros necesaria para la recuperación antes o durante la primera secuencia de restauración. Un grupo de archivos de solo lectura no necesita copias de seguridad de registros si se realizó una copia de seguridad de datos o diferencial después de haber configurado el grupo de archivos como de solo lectura.  
  
    > [!NOTE]  
    >  La información anterior se puede aplicar también a todos los archivos sin conexión.  
  
-   Un caso especial es un archivo de lectura/escritura que estaba en línea cuando se emitió la primera instrucción de restauración y que, a continuación, dicha instrucción dejó sin conexión automáticamente. En este caso, debe realizar una copia de seguridad de registros durante la primera *secuencia de restauración* (secuencia de una o varias instrucciones RESTORE que restauran, ponen al día y recuperan los datos). Por lo general, esta copia de seguridad de registros debe tener lugar después de que se hayan restaurado todas las copias de seguridad completas y antes de recuperar los datos. No obstante, si hay varias copias de seguridad de archivos para un grupo de archivos concreto, el punto mínimo de copia de seguridad de registros es después de que el grupo de archivos quede sin conexión. Esta copia de seguridad de registros posterior a la restauración de datos capta el punto en el que se dejó el archivo sin conexión y es necesaria porque [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no puede utilizar un registro en línea para una restauración en línea.  
  
    > [!NOTE]  
    >  Como alternativa, puede dejar el archivo sin conexión manualmente antes de la secuencia de restauración. Para obtener más información, vea "Dejar sin conexión una base de datos o un archivo" más adelante en este tema.  
  
##  <a name="taking-a-database-or-file-offline"></a><a name="taking_db_or_file_offline"></a> Dejar sin conexión una base de datos o un archivo  
 Si no desea utilizar la restauración en línea, puede dejar sin conexión la base de datos antes de iniciar la secuencia de restauración; para ello, puede usar uno de los métodos siguientes:  
  
-   En todos los modelos de recuperación puede dejar sin conexión la base de datos con la siguiente instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) :  
  
     ALTER DATABASE *nombre_base_de_datos* SET OFFLINE  
  
-   Si lo desea, en el modelo de recuperación completa, puede forzar que la restauración de un archivo o una página sea sin conexión; para ello, use la siguiente instrucción [BACKUP LOG](../../t-sql/statements/backup-transact-sql.md) la base de datos se pone en el estado de restauración:  
  
     BACKUP LOG *nombre_base_de_datos* WITH NORECOVERY.  
  
 Siempre que la base de datos permanezca sin conexión, todas las restauraciones serán sin conexión.  
  
## <a name="examples"></a>Ejemplos  
  
> [!NOTE]  
>  La sintaxis de un flujo de restauración en línea es la misma que la de un flujo de restauración sin conexión.  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Restaurar archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)  
  
-   [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
-   [Recuperar una base de datos sin restaurar los datos &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
-   [Quitar grupos de archivos inactivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Restauraciones de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Restauraciones de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)  
  
  
