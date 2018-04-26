---
title: 'Lección 9: Administración de conjuntos de copia de seguridad y copias de seguridad de instantáneas de archivos | Microsoft Docs'
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 766a0846-db15-4346-b814-4049039bcbfc
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ae8b4c3290b15b55d792f47186cefd3cc972f4b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-9-manage-backup-sets-and-file-snapshot-backups"></a>Lección 9: Administrar conjuntos de copia de seguridad y copias de seguridad de instantáneas de archivos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta lección, eliminará un conjunto de copia de seguridad mediante el procedimiento almacenado del sistema [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) . Este procedimiento almacenado del sistema elimina el archivo de copia de seguridad y el archivo de instantánea de cada archivo de base de datos asociado a este conjunto de copia de seguridad.  
  
> [!NOTE]  
> Si intenta eliminar un conjunto de copia de seguridad simplemente eliminando el archivo de copia de seguridad del contenedor de blobs de Azure, solo eliminará el archivo de copia de seguridad en sí y se conservarán las instantáneas de archivo asociadas. Si se encuentra en esta situación, use la función del sistema [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) para identificar la dirección URL de las instantáneas de archivos huérfanas y use el procedimiento almacenado del sistema [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para eliminar cada instantánea de archivos huérfanas. Para obtener más información, vea  [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
Para eliminar un conjunto de copia de seguridad de instantánea de archivos, siga estos pasos:  
  
1.  Conéctese a SQL Server Management Studio.  
  
2.  Abra una nueva ventana de consulta y conéctese a la instancia de SQL Server 2016 del motor de base de datos de la máquina virtual de Azure (o a cualquier instancia de SQL Server 2016 con permisos de lectura y escritura en este contenedor).  
  
3.  Copie y pegue el siguiente script de Transact-SQL en la ventana de consulta. Seleccione la copia de seguridad de registros que quiere eliminar junto con sus instantáneas de archivos asociadas. Modifique la dirección URL correctamente para su nombre de cuenta de almacenamiento y el contenedor que ha especificado en la lección 1, proporcione el nombre de archivo de la copia de seguridad de registros y ejecute este script.  
  
    ```  
  
    sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-9164-20150726012420.bak';  
  
    ```  
  
4.  En el Explorador de objetos, conéctese a Azure Storage.  
  
5.  Expanda los contenedores, expanda el contenedor creado en la lección 1 y compruebe que el archivo de copia de seguridad usado en el paso 3 ya no aparece en este contenedor (actualice el nodo si es necesario).  
  
    ![Contenedor de Azure que muestra la eliminación del blob de copia de seguridad de registros](../relational-databases/media/c0070b08-4667-4db5-aaff-987a404ec934.JPG "Contenedor de Azure que muestra la eliminación del blob de copia de seguridad de registros")  
  
6.  Copie, pegue y ejecute el siguiente script de Transact-SQL en la ventana de consulta para comprobar que se han eliminado dos instantáneas de archivos.  
  
    ```  
  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![Panel de resultados que muestra 2 instantáneas de archivos eliminadas](../relational-databases/media/f3891361-dfb6-4f4d-a090-ebfeb977981e.JPG "Panel de resultados que muestra 2 instantáneas de archivos eliminadas")  
  
**Final del tutorial**  
  
## <a name="see-also"></a>Ver también  
[Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
  

