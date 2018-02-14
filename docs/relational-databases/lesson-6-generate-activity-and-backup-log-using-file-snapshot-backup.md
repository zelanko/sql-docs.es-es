---
title: "Lección 6: Generación del registro de actividades y copias de seguridad mediante la copia de seguridad de instantáneas de archivos | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7deac98fa7bef4e087647aad142c735f01747c67
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup"></a>Lección 6: Generar el registro de actividades y copias de seguridad mediante la copia de seguridad de instantáneas de archivos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta lección, va a generar actividad en la base de datos AdventureWorks2014 y, periódicamente, va a crear copias de seguridad del registro de transacciones mediante copias de seguridad de instantáneas de archivos. Para obtener más información sobre las copias de seguridad de instantáneas de archivos, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para generar actividad en la base de datos AdventureWorks2014 y crear periódicamente copias de seguridad del registro de transacciones mediante copias de seguridad de instantáneas de archivos, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra dos nuevas ventanas de consulta y conecte cada una de ellas a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure.  
  
3.  Copie, pegue y ejecute el siguiente script de Transact-SQL en una de las ventanas de consulta. Tenga en cuenta que la tabla Production.Location tiene 14 filas antes de agregar nuevas filas en el paso 4.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
4.  Copie y pegue los dos siguientes scripts de Transact-SQL en las dos ventanas de consulta independientes. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1 y, después, ejecute estos scripts simultáneamente en ventanas de consulta independientes. Estos scripts tardarán unos siete minutos en completarse.  
  
    ```  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2014.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;  
  
    ```  
  
    ```  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2014.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2014 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  Revise el resultado del primer script y tenga en cuenta que el recuento final de filas ahora es de 29 939.  
  
    ![Se muestra un recuento de filas de 29 939.](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "Se muestra un recuento de filas de 29 939.")  
  
6.  Revise el resultado del segundo script y tenga en cuenta que cada vez que la instrucción BACKUP LOG se ejecuta, se crean dos nuevas instantáneas de archivos (una instantánea de archivo del archivo de registro y otra del archivo de datos) para un total de dos instantáneas de archivos para cada archivo de base de datos. Después de que se complete el segundo script, tenga en cuenta que ahora existen un total de 16 instantáneas de archivo, 8 para cada archivo de base de datos (uno de la instrucción BACKUP DATABASE y otro de cada ejecución de la instrucción BACKUP LOG).  
  
    ![Panel de resultados que muestra instantáneas de los archivos de datos y de registro al realizar la copia de seguridad de registros](../relational-databases/media/acd213b8-895e-425c-bd72-2bf10e65a5ba.JPG "Panel de resultados que muestra instantáneas de los archivos de datos y de registro al realizar la copia de seguridad de registros")  
  
    ![Se muestran cuatro instantáneas de archivos](../relational-databases/media/e7eff77d-85b9-4e52-abd8-e49952c8118a.JPG "Se muestran cuatro instantáneas de archivos")  
  
    ![Panel de resultados que muestra un total de 16 instantáneas de archivos](../relational-databases/media/c3ddff17-a83c-4bf0-a670-a38834f9c922.JPG "Panel de resultados que muestra un total de 16 instantáneas de archivos")  
  
7.  En el Explorador de objetos, conéctese a Azure Storage.  
  
8.  Expanda los contenedores, expanda el contenedor que ha creado en la lección 1 y compruebe que aparecen 7 nuevos archivos de copia de seguridad junto con los blobs de las lecciones anteriores (actualice el nodo según sea necesario).  
  
    ![Contenedor de Azure que muestra 7 blobs de copia de seguridad de registros](../relational-databases/media/cfa5a326-87a2-4202-9a04-38bf577d2d0b.JPG "Contenedor de Azure que muestra 7 blobs de copia de seguridad de registros")  
  
**Lección siguiente:**  
  
[Lección 7: Restaurar una base de datos a un momento dado](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
  
