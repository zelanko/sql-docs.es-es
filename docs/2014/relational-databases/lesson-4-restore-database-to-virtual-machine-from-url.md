---
title: Lección 5. Opta Cifrar la base de datos mediante TDE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fb9eaf62514b76e35b73ea87b7820751f670a90f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70175575"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>Lección 5. (Opcional) Cifrar la base de datos mediante TDE
  Como paso opcional, puede cifrar la base de datos creada recientemente. El cifrado de datos transparente (TDE) realiza el cifrado y descifrado de E/S en tiempo real de los datos y los archivos de registro. Este tipo de cifrado utiliza una clave de cifrado de la base de datos (DEK), que está almacenada en el registro de arranque de la base de datos para que esté disponible durante la recuperación. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](security/encryption/transparent-data-encryption.md) y [mueva una base de datos protegida por TDE a otra SQL Server](security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Azure Storage.  
  
-   Ha creado un contenedor en su cuenta de Azure Storage.  
  
-   Ha creado una directiva en un contenedor con derechos de lectura, escritura y enumeración. También generó una clave SAS.  
  
-   Ha creado una credencial de SQL Server en el equipo de origen.  
  
-   Ha creado una base de datos siguiendo los pasos descritos en la lección 4.  
  
 Si desea cifrar una base de datos, siga estos pasos:  
  
1.  En la máquina de origen, modifique y ejecute las instrucciones siguientes en una ventana de consulta:  
  
    ```  
  
    -- Create a master key and a server certificate   
    USE master   
    GO   
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01';   
    GO   
    CREATE CERTIFICATE MySQLCert WITH SUBJECT = 'SQL - Azure Storage Certification'   
    GO   
    -- Create a backup of the server certificate in the master database.   
    -- Store TDS certificates in the source machine locally.   
    BACKUP CERTIFICATE MySQLCert   
    TO FILE = 'C:\certs\MySQLCert.CER'   
    WITH PRIVATE KEY   
    (   
    FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
    ENCRYPTION BY PASSWORD = 'MySQLKey01'   
    );  
  
    ```  
  
2.  A continuación, cifre la nueva base de datos en el equipo de origen siguiendo estos pasos:  
  
    ```  
  
    -- Switch to the new database.   
    -- Create a database encryption key, that is protected by the server certificate in the master database.    
    -- Alter the new database to encrypt the database using TDE.   
    USE TestDB1;   
    GO   
    -- Encrypt your database   
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE MySQLCert   
    GO   
  
    ALTER DATABASE TestDB1   
    SET ENCRYPTION ON   
    GO  
  
    ```  
  
 Si desea obtener el estado de cifrado de una base de datos y sus claves de cifrado asociadas de la base de datos, ejecute la instrucción siguiente:  
  
```  
  
SELECT * FROM sys.dm_database_encryption_keys;   
GO  
  
```  
  
 Para obtener información detallada sobre las instrucciones Transact-SQL que se han utilizado en esta lección, vea [Create database &#40;SQL Server Transact-sql&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [ALTER DATABASE &#40;transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql), [Create Master Key &#40;Transact- ](/sql/t-sql/statements/create-master-key-transact-sql)sql&#41;, [CREATE Certificate &#40;transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)y [Sys. dm_database_encryption_keys &#40;Transact-SQL ](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)&#41;.  
  
 **Lección siguiente:**  
  
 [Lección 6: Migrar una base de datos desde un equipo de origen local a un equipo de destino en Azure](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
