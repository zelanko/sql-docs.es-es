---
title: Secuencias de restauración (modelo de recuperación completa) | Microsoft Docs
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 81f8e91f2179fdc0b11747714ab810b801dc5389
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75258660"
---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>Planear y realizar secuencias de restauración (modelo de recuperación completa)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se explica cómo planear y realizar una secuencia de restauración para bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa normalmente el modelo de recuperación completa. Una *secuencia de restauración* es una secuencia formada por una o varias instrucciones [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) . Por lo general, una secuencia de restauración inicializa el contenido de la base de datos, archivos y/o páginas que se van a restaurar (la fase de copia de datos), pone al día las transacciones registradas (fase de rehacer) y revierte las transacciones no confirmadas (fase de deshacer).  
  
 En los casos más sencillos, la secuencia de restauración solo requiere una copia de seguridad completa de la base de datos, una copia de seguridad diferencial de la base de datos y las copias de seguridad de registros subsiguientes. En estos casos, la creación de una secuencia de restauración correcta es fácil. Por ejemplo, para restaurar una base de datos completa al punto de error, empiece por hacer una copia de seguridad del registro de transacciones activo (el *tail* del registro). A continuación, restaure la copia de seguridad más reciente de la base de datos completa, la copia de seguridad diferencial más reciente (si la hay) y todas las copias de seguridad de registros subsiguientes en el orden en que se realizaron.  
  
 En casos más complejos, la creación de un flujo de restauración correcta puede ser un proceso complejo. Por ejemplo, una secuencia de restauración podría requerir varias copias de seguridad de archivos o la restauración de los datos a un momento dado. En casos muy complejos, podría ser necesario recorrer una ruta de recuperación bifurcada que abarque una o varias bifurcaciones de recuperación.  
  
> [!NOTE]  
>  Una *ruta de recuperación* es la secuencia de copias de seguridad de datos y de registros que sitúan la base de datos en un momento dado (denominado punto de recuperación). Una ruta de recuperación es un conjunto específico de transformaciones que han hecho evolucionar la base de datos a lo largo del tiempo manteniendo su coherencia. Una ruta de recuperación describe una serie de LSN desde un punto de inicio (LSN o GUID) hasta un extremo (LSN o GUID). La serie de LSN de una ruta de recuperación puede incluir una o varias ramas de recuperación desde el principio hasta el final.  
  
## <a name="to-plan-a-restore-sequence"></a>Para planear una secuencia de restauración  
 Antes de iniciar una secuencia de restauración, siga estos pasos:  
  
1.  Cree una copia del final del registro de la base de datos, si puede. Para obtener más información, vea [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
2.  Determine el punto de recuperación de destino.  
  
     El punto de recuperación de destino puede ser cualquier momento dado o cualquier marca de la copia de seguridad de un registro de transacciones. Para obtener más información, vea [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md) y [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
3.  Determine el tipo de restauración que desee realizar. Para obtener más información, vea [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
4.  Identifique qué copias de seguridad son necesarias y asegúrese de que están disponibles los conjuntos de medios y los dispositivos de copia de seguridad necesarios. Para obtener más información, vea [ Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md) y [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
## <a name="to-perform-a-restore-sequence"></a>Para realizar una secuencia de restauración  
 Para llevar a cabo una secuencia de restauración, siga estos pasos:  
  
1.  Para empezar la secuencia, restaure una o varias copias de seguridad de los datos, como una copia de seguridad de la base de datos, una copia de seguridad parcial, o una o varias copias de seguridad de archivos.  
  
2.  Si lo desea, restaure las copias de seguridad diferenciales más recientes que se basan en estas copias de seguridad completas.  
  
     Para cada copia de seguridad completa que piense restaurar, determine si es la base de alguna copia de seguridad diferencial. Si es así, restaure la copia de seguridad diferencial más reciente, si se puede. Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
3.  Ponga al día la base de datos mediante la restauración de las copias de seguridad de registros en secuencia, terminando con la copia de seguridad que contenga el punto de recuperación. Que tenga que aplicar todas las copias de seguridad de registros depende de la copia de seguridad de registros que contenga el punto de recuperación de destino, como se indica a continuación:  
  
    -   Si el punto de recuperación es el punto de un error, debe restaurar todas las copias de seguridad de registros creadas desde la última copia de seguridad (completa o diferencial) de datos restaurada. Para obtener más información, vea [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
    -   Para las restauraciones a un momento dado, podría no necesitar las copias de seguridad de registros más recientes. Si usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el Asesor para recuperación de base de datos se asegura de que solo estén seleccionadas las copias de seguridad necesarias para restaurar al momento que ha especificado. Estas copias de seguridad componen el plan de restauraciones recomendado para la restauración a un momento dado. Para obtener más información, vea [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="restarting-a-restore-sequence"></a>Reiniciar una secuencia de restauración  
 Si encuentra algún problema con el resultado de una secuencia de restauración, puede salir de ella y reiniciarla desde el principio. Por ejemplo, si accidentalmente restaura demasiadas copias de seguridad de registros y se supera el punto de recuperación deseado, debe reiniciar la secuencia de restauración hasta la copia de seguridad de registros que contenga el punto de recuperación de destino.  
  
## <a name="see-also"></a>Consulte también  
 [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
