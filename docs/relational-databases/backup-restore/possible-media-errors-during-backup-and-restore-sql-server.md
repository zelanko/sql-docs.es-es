---
title: "Errores posibles de medios durante copia de seguridad y restauración (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- media errors [SQL Server]
- CONTINUE_AFTER_ERROR option
- errors [SQL Server], backups
- backups [SQL Server], errors
- RESTORE VERIFYONLY statement
- backup media [SQL Server], error management
- page checksums [SQL Server]
- backup checksums [SQL Server]
- backing up [SQL Server], media errors
- RESTORE statement, media errors
- NO_CHECKSUM option
- checksums [SQL Server]
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 39ab370ba08f99d15e43ad88429e1cb72946562b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="possible-media-errors-during-backup-and-restore-sql-server"></a>Errores posibles de medios durante copia de seguridad y restauración (SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ofrece la opción de recuperación de una base de datos a pesar de los errores detectados. Un importante mecanismo de detección de errores nuevo es la creación opcional de una suma de comprobación de copia de seguridad que se puede crear mediante una operación de copia de seguridad y validar mediante una operación de restauración. Puede controlar si una operación comprueba si hay errores y si la operación se detiene o continúa al encontrar un error. Si una copia de seguridad contiene una suma de comprobación de copia de seguridad, las instrucciones RESTORE y RESTORE VERIFYONLY pueden comprobar si hay errores.  
  
> [!NOTE]  
>  Las copias de seguridad reflejadas proporcionan hasta cuatro copias (reflejos) de un conjunto de medios, ofreciendo copias alternativas para recuperar el sistema de los errores provocados por los medios dañados. Para obtener más información, vea [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md).  
  
  
##  <a name="BckChecksums"></a> Comprobaciones de copia de seguridad  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite tres tipos de sumas de comprobación: una suma de comprobación de páginas, una de bloques de registro y una de copia de seguridad. Al generar una suma de comprobación de copia de seguridad, BACKUP comprueba que los datos que se leen de la base de datos son coherentes con cualquier suma de comprobación o indicación de página rasgada de la base de datos.  
  
 La instrucción BACKUP calcula opcionalmente una suma de comprobación de copia de seguridad en el flujo de copia de seguridad; si hay una suma de comprobación de página o información de página rasgada en determinada página, al hacer la copia de seguridad de la página, BACKUP comprueba también el estado de página rasgada, la suma de comprobación y el Id. de la página. Al crear una suma de comprobación de copia de seguridad, una operación de copia de seguridad no agrega sumas de comprobación a las páginas. Las páginas se copian tal y como están en la base de datos y la copia de seguridad no las modifica.  
  
 Debido a la carga que supone comprobar y generar sumas de comprobación de seguridad, su utilización puede tener consecuencias negativas sobre el rendimiento. Pueden quedar afectados tanto la carga de trabajo como el rendimiento de la copia de seguridad. Por consiguiente, el uso de la suma de comprobación de copia de seguridad es opcional. Cuando decida si va a generar sumas de comprobación durante una copia de seguridad, supervise cuidadosamente la sobrecarga de CPU en la que se incurrirá, así como el impacto sobre las posibles cargas de trabajo simultáneas del sistema.  
  
 BACKUP no modifica nunca la página de origen del disco ni el contenido de una página.  
  
 Cuando se habilitan las sumas de comprobación de copia de seguridad, una operación de copia de seguridad realiza los siguientes pasos:  
  
1.  Antes de escribir una página en los medios de copia de seguridad, la operación de copia de seguridad comprueba la información en el nivel de página (suma de comprobación de página o detección de página rasgada), si existe. Si no existe, la copia de seguridad no puede comprobar la página. Las páginas no comprobadas se incluyen tal cual y su contenido se agrega a la suma de comprobación de copia de seguridad total.  
  
     Si la operación de copia de seguridad encuentra un error de página durante la comprobación, la copia de seguridad genera un error.  
  
    > [!NOTE]  
    >  Para obtener más información acerca de las sumas de comprobación de página y la detección de página rasgada, vea la opción PAGE_VERIFY de la instrucción ALTER DATABASE. Para obtener más información, vea [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
2.  Aunque se incluyan sumas de comprobación de página, BACKUP genera una suma de comprobación de copia de seguridad independiente para las secuencias de copia de seguridad. Opcionalmente, las operaciones de restauración pueden utilizar la suma de comprobación de copia de seguridad para confirmar que la copia de seguridad no está dañada. La suma de comprobación de copia de seguridad se almacena en el medio de copia de seguridad y no en las páginas de la base de datos. La suma de comprobación de copia de seguridad se puede utilizar opcionalmente en el momento de la restauración.  
  
3.  El conjunto de copia de seguridad se marca para indicar que contiene sumas de comprobación de copia de seguridad (en la columna **has_backup_checksums** de **msdb..backupset)**. Para obtener más información, vea [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
 Durante una operación de restauración, si hay sumas de comprobación de copia de seguridad en los medios de copia de seguridad, de forma predeterminada, las operaciones RESTORE y RESTORE VERIFYONLY comprueban las sumas de comprobación de copia de seguridad y las sumas de comprobación de página. Si no hay ninguna suma de comprobación de copia de seguridad, cualquiera de las dos operaciones de restauración continúa sin realizar ninguna comprobación; esto se debe a que, sin una suma de comprobación de copia de seguridad, la restauración no puede comprobar de forma confiable las sumas de comprobación de página.  
  
## <a name="response-to-page-checksum-errors-during-a-backup-or-restore-operation"></a>Respuesta a errores de suma de comprobación de página durante una operación de copia de seguridad o restauración  
 De forma predeterminada, después de encontrar un error de suma de comprobación de página, una operación BACKUP o RESTORE produce un error y una operación VERIFYONLY continúa. Sin embargo, se puede controlar si una operación dada se detiene al encontrar un error o continúa de la mejor manera posible.  
  
 Si una operación BACKUP continúa después de encontrar errores, la operación realiza los siguientes pasos:  
  
1.  Indica en el conjunto de copia de seguridad de los medios de copia de seguridad que hay errores y realiza el seguimiento de la página en la tabla **suspect_pages** de la base de datos **msdb**. Para obtener más información, vea [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md).  
  
2.  Registra el error en el registro de errores de SQL Server.  
  
3.  Marca el conjunto de copia de seguridad como conjunto que contiene este tipo de error (en la columna **is_damaged** de **msdb.backupset)**. Para obtener más información, vea [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
4.  Emite un mensaje que indica que la copia de seguridad se generó correctamente, pero contiene errores de página.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para habilitar o deshabilitar sumas de comprobación de copia de seguridad**  
  
-   [Habilitar o deshabilitar sumas de comprobación de copia de seguridad durante copia de seguridad o restauración &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **Para controlar la respuesta a un error durante una operación de copia de seguridad**  
  
-   [Especificar si una operación de copia de seguridad o restauración continúa o se detiene después de encontrar un error &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
  
