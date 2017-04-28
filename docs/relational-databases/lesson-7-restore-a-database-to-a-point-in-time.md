---
title: "Lección 7: Restauración de una base de datos a un momento dado | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a25788a3b7eda518aeff01329eb5e207d9092bd6
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-7-restore-a-database-to-a-point-in-time"></a>Lección 7: Restaurar una base de datos a un momento dado
En esta lección, restaurará la base de datos AdventureWorks2014 a un momento dado entre dos de las copias de seguridad del registro de transacciones.  
  
Con las copias de seguridad tradicionales, para lograr una restauración a un momento dado, necesitará usar la copia de seguridad de la base de datos completa, quizás una copia de seguridad diferencial y todos los archivos de registro de transacciones hasta el momento dado y justo después del momento dado al que quiere restaurar. Con las copias de seguridad de instantáneas de archivos, solo necesita los dos archivos de copia de seguridad de registros adyacentes que proporcionan los objetivos que enmarcan el momento al que quiere restaurar. Solo necesita dos conjuntos de copia de seguridad de registros de instantáneas de archivos, porque cada copia de seguridad de registros crea una instantánea de archivo de cada archivo de base de datos (cada archivo de datos y el archivo de registro).  
  
Para restaurar una base de datos a un momento dado a partir de conjuntos de copia de seguridad de instantáneas de archivos, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure.  
  
3.  Copie, pegue y ejecute el siguiente script de Transact-SQL en la ventana de consulta. Compruebe que la tabla Production.Location tiene 29 939 filas antes de restaurarla a un momento dado en el que tiene menos filas en el paso 5.  
  
    ```  
  
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location  
  
    ```  
  
    ![Se muestra un recuento de filas de 29 939.](../relational-databases/media/5e2f4229-1970-49c9-89b3-e96b6f7fde83.JPG "Se muestra un recuento de filas de 29 939.")  
  
4.  Copie y pegue el siguiente script de Transact-SQL en la ventana de consulta. Seleccione dos archivos de copia de seguridad de registros adyacentes y convierta el nombre de archivo en la fecha y hora que necesitará para este script. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1, proporcione el primer y segundo nombre de archivo de copia de seguridad, proporcione el momento STOPAT en el formato "26 de junio, 2015 01:48 p. m." y, después, ejecute este script. Este script tardará unos minutos en completarse  
  
    ```  
  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2014 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2014   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2015 01:48 PM';  
    ALTER DATABASE AdventureWorks2014 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2014.Production.Location ;  
  
    ```  
  
5.  Revise el resultado. Observe que, después de la restauración, el recuento de filas es 18 389, que es un número de recuento de filas entre la copia de seguridad de registros 5 y 6 (su recuento de filas puede variar).  
  
    ![Panel de resultados que muestra el recuento de filas después de la restauración a un momento dado](../relational-databases/media/4a0c6d8b-e2ed-4e93-bd7a-ade22a4aecc6.JPG "Panel de resultados que muestra el recuento de filas después de la restauración a un momento dado")  
  
**Lección siguiente:**  
  
[Lesson 8: Restore as new database from log backup](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md) (Lección 8: Restaurar como una base de datos nueva desde una copia de seguridad de registros)  
  
  
  

