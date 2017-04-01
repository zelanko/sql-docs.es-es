---
title: "Ejemplo: restauraci&#243;n por etapas exclusiva para algunos grupos de archivos (modelo de recuperaci&#243;n simple) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "restauraciones por etapas [SQL Server], modelo de recuperación simple"
  - "secuencias de restauración [SQL Server], por etapas"
  - "modelo de recuperación simple [SQL Server], ejemplos de RESTORE"
ms.assetid: d7ad026c-5355-4308-9560-0dc843940d4f
caps.latest.revision: 28
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 28
---
# Ejemplo: restauraci&#243;n por etapas exclusiva para algunos grupos de archivos (modelo de recuperaci&#243;n simple)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema solo es relevante para las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el modelo de recuperación simple que contienen un grupo de archivos de solo lectura.  
  
 En una secuencia de restauración por etapas restaura y recupera una base de datos en fases en el nivel del grupo de archivos, empezando con los grupos de archivos principales y todos los secundarios de lectura/escritura.  
  
 En este ejemplo, una base de datos llamada `adb`, que utiliza el modelo de recuperación simple, contiene tres grupos de archivos. El grupo de archivos `A` es de lectura/escritura, mientras que los grupos de archivos `B` y `C` son de solo lectura. Inicialmente, todos los grupos de archivos están en línea.  
  
 Parece que los grupos de archivos principal y `B` de la base de datos `adb` están dañados; por lo tanto, el administrador de la base de datos decide restaurarlos mediante una secuencia de restauración por etapas. En un modelo de recuperación simple, todos los grupos de archivos de lectura/escritura deben restaurarse desde la misma copia de seguridad parcial. Aunque el grupo de archivos `A` está intacto, debe restaurarse con el grupo de archivos principal para garantizar que sean coherentes (la base de datos se restaurará al momento definido por el final de la última copia de seguridad parcial). El grupo de archivos `C` está intacto, pero debe recuperarlo para ponerlo en línea. El grupo de archivos `B`, aunque está dañado, contiene menos datos críticos que el grupo de archivos `C`; por tanto, `B` será el último en restaurarse.  
  
## Secuencias de restauración  
  
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
  
     Deben restaurarse los archivos del grupo de archivos `B`. El administrador de la base de datos restaura la copia de seguridad del grupo de archivos `B` realizada después de que el grupo de archivos `B` pasara a ser de solo lectura y antes de la copia de seguridad parcial.  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup   
    WITH RECOVERY  
    ```  
  
     Todos los grupos de archivos están ahora en línea.  
  
## Otros ejemplos  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas de base de datos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de lectura/escritura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [Ejemplo: restauración con conexión de un archivo de solo lectura &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## Vea también  
 [Restauración con conexión &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Restauraciones por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  