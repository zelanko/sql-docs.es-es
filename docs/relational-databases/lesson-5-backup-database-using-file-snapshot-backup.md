---
title: "Lección 5: Realización de una copia de seguridad de la base de datos mediante la copia de seguridad de instantáneas de archivos | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
caps.latest.revision: "19"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b5e0888f00f34fc3d85f6727cc98903c66c2239
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-backup-database-using-file-snapshot-backup"></a>Lesson 5: Backup database using file-snapshot backup (Lección 5: Realizar una copia de seguridad de la base de datos mediante la copia de seguridad de instantáneas de archivos)
En esta lección, realizará una copia de seguridad de la base de datos AdventureWorks2014 en la máquina virtual de Azure mediante la copia de seguridad de instantáneas de archivos para realizar una copia de seguridad casi inmediata mediante instantáneas de Azure. Para obtener más información sobre las copias de seguridad de instantáneas de archivos, consulte [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
  
Para realizar una copia de seguridad de la base de datos AdventureWorks2014 mediante la copia de seguridad de instantáneas de archivos, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure.  
  
3.  Copie, pegue y ejecute el siguiente script de Transact-SQL en la ventana de consulta (no cierre esta ventana de consulta: ejecutará este script nuevo en el paso 5). Este procedimiento almacenado del sistema permite ver las copias de seguridad de instantáneas de archivos existentes para cada archivo que forma parte de una base de datos especificada. Observará que no hay copias de seguridad de instantáneas de archivos para esta base de datos.  
  
    ```  
  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
4.  Copie y pegue el siguiente script de Transact-SQL en la ventana de consulta. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1 y, después, ejecute este script. Observe la rapidez con la que se crea esta copia de seguridad.  
  
    ```  
  
    -- Backup the AdventureWorks2014 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_Azure.bak'   
       WITH FILE_SNAPSHOT;  
  
    ```  
  
    ![Panel de resultados que muestra instantáneas de archivos para cada archivo de base de datos](../relational-databases/media/2a9320e0-067a-485a-8e0e-636660005e5c.JPG "Panel de resultados que muestra instantáneas de archivos para cada archivo de base de datos")  
  
5.  Después de comprobar que el script del paso 4 se ha ejecutado correctamente, ejecute el siguiente script de nuevo. Observe que la operación de copia de seguridad de instantáneas de archivos en el paso 4 genera instantáneas de archivo de los datos y del archivo de registro.  
  
    ```  
  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![Resultados de la función sys.fn_db_backup_file_snapshots en la que se muestran 2 instantáneas](../relational-databases/media/fca1436e-9607-4432-97ee-f66ac2f2108d.JPG "Resultados de la función sys.fn_db_backup_file_snapshots en la que se muestran 2 instantáneas")  
  
6.  En el Explorador de objetos, en la instancia de SQL Server 2016 en la máquina virtual de Azure, expanda el nodo Bases de datos y compruebe que se ha restaurado la base de datos AdventureWorks2014 a esta instancia (actualice el nodo según sea necesario).  
  
7.  En el Explorador de objetos, conéctese a Azure Storage.  
  
8.  Expanda Contenedores, expanda el contenedor que creó en la Lección 1 y compruebe que la AdventureWorks2014_Azure.bak del paso 4 anterior aparece en este contenedor, junto con el archivo de copia de seguridad de la Lección 3 y los archivos de base de datos de la Lección 4 (actualice el nodo según sea necesario).  
  
    ![Copia de seguridad de instantáneas de archivos que aparecen en el contenedor de Azure](../relational-databases/media/181bc970-4af7-4272-a9ae-4bef674f2e02.JPG "Copia de seguridad de instantáneas de archivos que aparecen en el contenedor de Azure")  
  
**Lección siguiente:**  
  
[Lección 6: Generar el registro de actividades y copias de seguridad mediante la copia de seguridad de instantáneas de archivos](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
## <a name="see-also"></a>Vea también  
[Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
  
  
  
