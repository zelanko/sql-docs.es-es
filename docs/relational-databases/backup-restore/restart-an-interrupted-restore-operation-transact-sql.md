---
title: "Reiniciar una operaci&#243;n de restauraci&#243;n interrumpida (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "operación de restauración interrumpida"
  - "restaurar bases de datos [SQL Server], reiniciar una operación interrumpida"
  - "restablecer las opciones cambiadas después de la copia de seguridad"
  - "restaurar bases de datos [SQL Server], reiniciar una operación interrumpida"
  - "reiniciar una operación de restauración interrumpida"
  - "restaurar una operación interrumpida [SQL Server]"
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Reiniciar una operaci&#243;n de restauraci&#243;n interrumpida (Transact-SQL)
  En este tema se explica el modo de reiniciar una operación de restauración interrumpida.  
  
### Para reiniciar una operación de restauración interrumpida  
  
1.  Ejecute de nuevo la instrucción RESTORE interrumpida especificando:  
  
    -   Las mismas cláusulas utilizadas en la instrucción RESTORE original.  
  
    -   La cláusula RESTART.  
  
## Ejemplo  
 Este ejemplo reinicia una operación de restauración interrumpida.  
  
```tsql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## Vea también  
 [Restauraciones de base de datos completas &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)  
  
  