---
title: Restaurar una base de datos al punto de error en el modelo de recuperación completa (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- point of failure [SQL Server]
- restoring databases [SQL Server], point of failure
- database restores [SQL Server], point of failure
ms.assetid: 04106e18-bbf7-4a5e-a2e1-3d65319814d5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83319e8eb1fe692bc55b764445ac155d9e1ad38d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62920991"
---
# <a name="restore-a-database-to-the-point-of-failure-under-the-full-recovery-model-transact-sql"></a>Restaurar una base de datos según el punto de error en el modelo de recuperación completa (Transact-SQL)
  En este tema se explica cómo realizar una restauración hasta el momento del error. Este tema solo es relevante para las bases de datos que utilizan los modelos de recuperación completa u optimizado para cargas masivas de registros.  
  
### <a name="to-restore-to-the-point-of-failure"></a>Para restaurar hasta el momento del error  
  
1.  Realice una copia de seguridad del final del registro mediante la ejecución de la siguiente instrucción [BACKUP](/sql/t-sql/statements/backup-transact-sql) básica:  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  Restaure una copia de seguridad completa de la base de datos mediante la ejecución de la siguiente instrucción [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) básica:  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
3.  Opcionalmente, restaure una copia de seguridad diferencial de la base de datos mediante la ejecución de la siguiente instrucción RESTORE DATABASE básica:  
  
    ```  
    RESTORE DATABASE <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
4.  Aplique los registros de transacciones, incluida la copia del final del registro que ha creado en el paso 1, mediante la especificación de WITH NORECOVERY en la instrucción RESTORE LOG:  
  
    ```  
    RESTORE LOG <database_name> FROM <backup_device>   
       WITH NORECOVERY;  
    ```  
  
5.  Recupere la base de datos mediante la ejecución de la siguiente instrucción RESTORE DATABASE:  
  
    ```  
    RESTORE DATABASE <database_name>   
       WITH RECOVERY;  
    ```  
  
## <a name="example"></a>Ejemplo  
 Antes de que pueda ejecutar el ejemplo, debe completar los preparativos siguientes:  
  
1.  La base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] utiliza el modelo de recuperación simple de forma predeterminada. Puesto que este modelo de recuperación no admite la restauración hasta el punto del error, configure [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para que utilice el modelo de recuperación completa mediante la ejecución de la siguiente instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) :  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
    ```  
  
2.  Cree una copia de seguridad completa de la base de datos mediante la siguiente instrucción BACKUP:  
  
    ```  
    BACKUP DATABASE AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Data.bck';  
    ```  
  
3.  Cree una copia de seguridad de registros rutinaria:  
  
    ```  
    BACKUP LOG AdventureWorks2012 TO DISK = 'C:\AdventureWorks2012_Log.bck';  
    ```  
  
 En el ejemplo siguiente se restauran las copias de seguridad que se han creado con anterioridad, tras crear una copia del final del registro de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . (En este paso se asume que se puede tener acceso al disco de registros).  
  
 Primero, en el ejemplo se crea una copia del final del registro de la base de datos que captura el registro activo y deja la base de datos en el estado de restauración. A continuación, en el ejemplo se restaura la copia de seguridad de la base de datos, se aplica la copia del final del registro rutinaria que se ha creado con anterioridad y se aplica la copia de seguridad de registros después del error. Finalmente, en el ejemplo se recupera la base de datos en un paso diferente.  
  
> [!NOTE]  
>  El comportamiento predeterminado es recuperar una base de datos como parte de la instrucción que restaura la copia de seguridad final.  
  
```  
/* Example of restoring a to the point of failure */  
-- Step 1: Create a tail-log backup by using WITH NORECOVERY.  
BACKUP LOG AdventureWorks2012  
   TO DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 2: Restore the full database backup.  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Data.bck'  
   WITH NORECOVERY;  
GO  
-- Step 3: Restore the first transaction log backup.  
RESTORE LOG AdventureWorks2012  
   FROM DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 4: Restore the tail-log backup.  
RESTORE LOG AdventureWorks2012  
   FROM  DISK = 'C:\AdventureWorks2012_Log.bck'  
   WITH NORECOVERY;  
GO  
-- Step 5: Recover the database.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
