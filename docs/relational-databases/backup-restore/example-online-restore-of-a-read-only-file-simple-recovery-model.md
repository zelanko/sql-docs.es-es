---
title: "Ejemplo: restauración en línea de un archivo de solo lectura (modelo de recuperación simple) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restore sequences [SQL Server], online
- online restores [SQL Server], simple recovery model
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 0c691fc6-9865-46a7-b055-8097424492d6
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 54c06105b3d073c3bfa9543db4c3ff96445db536
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="example-online-restore-of-a-read-only-file-simple-recovery-model"></a>Ejemplo: restauración en línea de un archivo de solo lectura (modelo de recuperación simple)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema solo es relevante para las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el modelo de recuperación simple que contienen un grupo de archivos de solo lectura. El modelo de recuperación simple permite restaurar un archivo de solo lectura en línea si existe una copia de seguridad realizada después de que el archivo pasara a ser de solo lectura por última vez.  
  
 En este ejemplo, la base de datos `adb` contiene tres grupos de archivos. El grupo de archivos `A` es de lectura/escritura, mientras que los grupos de archivos `B` y `C` son de solo lectura. Inicialmente, todos los grupos de archivos están en línea. Se debe restaurar el archivo de solo lectura `B`del grupo de archivos `b1`. El administrador de la base de datos puede restaurarlo mediante una copia de seguridad realizada después de que el archivo pasara a ser de solo lectura. Durante la restauración, el grupo de archivos `B` permanecerá sin conexión, pero el resto de la base de datos estará en línea.  
  
## <a name="restore-sequence"></a>Secuencia de restauración  
  
> [!NOTE]  
>  La sintaxis de un flujo de restauración en línea es la misma que la de un flujo de restauración sin conexión.  
  
 Para restaurar el archivo, el administrador de la base de datos utiliza la siguiente secuencia de restauración:  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup   
WITH RECOVERY  
```  
  
 Ahora el archivo está en línea.  
  
## <a name="additional-examples"></a>Otros ejemplos  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>Vea también  
 [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Restauraciones de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
