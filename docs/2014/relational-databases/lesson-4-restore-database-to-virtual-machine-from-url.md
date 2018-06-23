---
title: Lección 5. (Opcional) Cifrar la base de datos con TDE | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c8ef2e904c197822721a5c48f811a2a895b5ca59
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202946"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>Lección 5. (Opcional) Cifrar la base de datos mediante TDE
  Como paso opcional, puede cifrar la base de datos creada recientemente. El cifrado de datos transparente (TDE) realiza el cifrado y descifrado de E/S en tiempo real de los datos y los archivos de registro. Este tipo de cifrado utiliza una clave de cifrado de la base de datos (DEK), que está almacenada en el registro de arranque de la base de datos para que esté disponible durante la recuperación. Para obtener más información, consulte [cifrado de datos transparente &#40;TDE&#41; ](security/encryption/transparent-data-encryption.md) y [mover una base de datos protegida de TDE a otro servidor SQL Server](security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
 En esta lección se supone que ya completó los pasos siguientes:  
  
-   Tiene una cuenta de Almacenamiento de Windows Azure.  
  
-   Ha creado un contenedor con su cuenta de Almacenamiento de Windows Azure.  
  
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
  
 For detailed information the Transact-SQL statements that have been used in this lesson, see [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql), [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql), [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql), and [sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql).  
  
 **Lección siguiente:**  
  
 [Lección 6: Migrar una base de datos de un origen de la máquina local a una máquina de destino en Windows Azure](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
