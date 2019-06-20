---
title: 'Ejemplo: Restauración por etapas de sólo algunos grupos de archivos (modelo de recuperación Simple) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7cdc7e6c036a38ac40eb8c7bb2495b1ed5a3e6e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62922038"
---
# <a name="example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model"></a>Ejemplo: Restauración por etapas exclusiva para algunos grupos de archivos (modelo de recuperación simple)
  Este tema solo es relevante para las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el modelo de recuperación simple que contienen un grupo de archivos de solo lectura.  
  
 En una secuencia de restauración por etapas restaura y recupera una base de datos en fases en el nivel del grupo de archivos, empezando con los grupos de archivos principales y todos los secundarios de lectura/escritura.  
  
 En este ejemplo, una base de datos llamada `adb`, que utiliza el modelo de recuperación simple, contiene tres grupos de archivos. El grupo de archivos `A` es de lectura/escritura, mientras que los grupos de archivos `B` y `C` son de solo lectura. Inicialmente, todos los grupos de archivos están en línea.  
  
 Parece que los grupos de archivos principal y `B` de la base de datos `adb` están dañados; por lo tanto, el administrador de la base de datos decide restaurarlos mediante una secuencia de restauración por etapas. En un modelo de recuperación simple, todos los grupos de archivos de lectura/escritura deben restaurarse desde la misma copia de seguridad parcial. Aunque el grupo de archivos `A` está intacto, debe restaurarse con el grupo de archivos principal para garantizar que sean coherentes (la base de datos se restaurará al momento definido por el final de la última copia de seguridad parcial). El grupo de archivos `C` está intacto, pero debe recuperarlo para ponerlo en línea. El grupo de archivos `B`, aunque está dañado, contiene menos datos críticos que el grupo de archivos `C`; por tanto, `B` será el último en restaurarse.  
  
## <a name="restore-sequences"></a>Secuencias de restauración  
  
> [!NOTE]  
>  La sintaxis de un flujo de restauración en línea es la misma que la de un flujo de restauración sin conexión.  
  
1.  Restauración parcial de los grupos de archivos principal y `A` desde una copia de seguridad parcial.  
  
    ```  
    RESTORE DATABASE adb READ_WRITE_FILEGROUPS FROM partial_backup   
    WITH PARTIAL, RECOVERY  
    ```  
  
     En este momento, los grupos de archivos principal y `A` están en línea. La recuperación de los archivos de los grupos `B` y `C` está pendiente, por lo que estos grupos de archivo están sin conexión.  
  
2.  Recuperación en línea del grupo de archivos `C`.  
  
     El grupo de archivos `C` es coherente porque la copia de seguridad parcial restaurada anteriormente se realizó después de que `C` pasara a ser de solo lectura, aunque la restauración hizo que la base de datos pasase a un punto anterior. El administrador de la base de datos recupera el grupo de archivos `C`, sin restaurarlo, y lo conecta.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='C' WITH RECOVERY  
    ```  
  
     En este momento, los grupos de archivos principal, `A` y `C` están en línea. Los archivos del grupo B permanecen pendientes de recuperación, con el grupo de archivos sin conexión.  
  
3.  Restauración en línea del grupo de archivos `B.`  
  
     Deben restaurarse los archivos del grupo de archivos `B` . El administrador de la base de datos restaura la copia de seguridad del grupo de archivos `B` realizada después de que el grupo de archivos `B` pasara a ser de solo lectura y antes de la copia de seguridad parcial.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     Todos los grupos de archivos están ahora en línea.  
  
## <a name="additional-examples"></a>Otros ejemplos  
  
-   [Ejemplo: restauración por etapas de la base de datos &#40;modelo de recuperación simple&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de la base de datos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vea también  
 [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
