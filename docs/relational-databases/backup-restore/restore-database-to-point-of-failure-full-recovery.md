---
title: 'Restauración de la base de datos en el punto de error: recuperación completa'
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
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
ms.openlocfilehash: 5cf3638c1f79c560abd96c262f4ff2c23e312d09
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75241860"
---
# <a name="restore-database-to-point-of-failure---full-recovery"></a>Restaurar la base de datos en el punto de error: Recuperación completa
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se explica cómo realizar una restauración hasta el momento del error. Este tema solo es relevante para las bases de datos que utilizan los modelos de recuperación completa u optimizado para cargas masivas de registros.  
  
### <a name="to-restore-to-the-point-of-failure"></a>Para restaurar hasta el momento del error  
  
1.  Realice una copia de seguridad del final del registro mediante la ejecución de la siguiente instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md) básica:  
  
    ```  
    BACKUP LOG <database_name> TO <backup_device>   
       WITH NORECOVERY, NO_TRUNCATE;  
    ```  
  
2.  Restaure una copia de seguridad completa de la base de datos mediante la ejecución de la siguiente instrucción [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md) básica:  
  
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
  
1.  La base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] utiliza el modelo de recuperación simple de forma predeterminada. Puesto que este modelo de recuperación no admite la restauración hasta el punto del error, configure [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para que utilice el modelo de recuperación completa mediante la ejecución de la siguiente instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) :  
  
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
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
