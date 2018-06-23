---
title: 'Ejemplo: restauración por etapas de la base de datos (modelo de recuperación simple) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5725d193db83cb2648d1676cf99662af65a543d2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199704"
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>Ejemplo: restauración por etapas de base de datos (modelo de recuperación simple)
  En una secuencia de restauración por etapas restaura y recupera una base de datos en fases en el nivel del grupo de archivos, empezando con los grupos de archivos principales y todos los secundarios de lectura/escritura.  
  
 En este ejemplo, la base de datos `adb` se restaura en un nuevo equipo después de un desastre. La base de datos utiliza el modelo de recuperación simple. Antes del desastre, todos los grupos de archivos están en línea. Los grupos de archivos `A` y `C` son de lectura/escritura, y el grupo de archivos `B` es de solo lectura. El grupo de archivos `B` pasó a ser de solo lectura antes de la copia de seguridad parcial más reciente, que contiene el grupo de archivos principal y los grupos de archivos secundarios de lectura/escritura, `A` y `C`. Después de que el grupo de archivos `B` pasara a ser de solo lectura, se realizó una copia de seguridad de archivos independiente del grupo de archivos `B` .  
  
## <a name="restore-sequences"></a>Secuencias de restauración  
  
1.  Restauración parcial del grupo de archivos principal y los grupos de archivos `A` y `C`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     En este momento, los grupos de archivos principal, `A` y `C` están en línea. Todos los archivos del grupo de archivos `B` están pendientes de recuperación y el grupo de archivos está sin conexión.  
  
2.  Restauración con conexión del grupo de archivos `B`.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     Todos los grupos de archivos están ahora en línea.  
  
## <a name="additional-examples"></a>Otros ejemplos  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vea también  
 [Restauración con conexión &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Restauraciones por etapas &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
