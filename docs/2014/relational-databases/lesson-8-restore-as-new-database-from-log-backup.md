---
title: Lección 9. Restaurar una base de datos de almacenamiento de Windows Azure | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b8ff5ec90f80262aae76abfb01ef6c737d13369c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204178"
---
# <a name="lesson-9-restore-a-database-from-windows-azure-storage"></a>Lección 9. Restaurar una base de datos desde Azure Storage
  En esta lección, aprenderá a restaurar un archivo de copia de seguridad de la base de datos de Azure Storage en una base de datos, que reside en local o en una máquina virtual de Microsoft Azure. Para seguir esta lección, no es necesario completar las lecciones 4, 5, 6, 7 y 8.  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Ha creado una base de datos en el equipo de origen.  
  
-   Ha creado una copia de seguridad de la base de datos (.bak) en almacenamiento de Windows Azure con el [SQL Server Backup and Restore con el servicio de almacenamiento de blobs de Windows Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) característica. Tenga en cuenta que deberá crear una credencial de SQL Server en este paso. Esta credencial utiliza las claves de la cuenta de almacenamiento.  
  
-   Tiene una cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado un contenedor con su cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo para la característica de integración de Azure Storage. Observe que esta credencial requiere una clave de la firma de acceso compartido (SAS).  
  
 Para restaurar una base de datos desde Azure Storage, puede seguir estos pasos:  
  
1.  Inicie SQL Server Management Studio. Conéctese a la instancia predeterminada.  
  
2.  Haga clic en **nueva consulta** en la barra de herramientas estándar.  
  
3.  Copie y pegue el script completo siguiente en la ventana de consultas. Modifique el script según sea necesario.  
  
     **Nota:** ejecutar el `RESTORE` instrucción para restaurar la copia de seguridad de base de datos (.bak) en almacenamiento de Windows Azure a una instancia de base de datos en otro equipo.  
  
    ```tsql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Windows Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Windows Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **Final del Tutorial: archivos de datos SQL Server en el servicio de almacenamiento de Windows Azure**  
  
  