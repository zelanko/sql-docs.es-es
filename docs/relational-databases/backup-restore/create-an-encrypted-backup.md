---
title: Creación de una copia de seguridad cifrada | Microsoft Docs
description: En este artículo se muestra cómo crear una copia de seguridad cifrada en SQL Server mediante Transact-SQL. Se puede realizar una copia de seguridad en disco o en Azure Storage.
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a235ae2c396334d7dbd7c27efb582bf8c1890219
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748437"
---
# <a name="create-an-encrypted-backup"></a>Crear una copia de seguridad cifrada
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describen los pasos necesarios para crear una copia de seguridad cifrada mediante Transact-SQL.  Para ver un ejemplo que usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Crear una copia de seguridad completa de base de datos (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md). 
  
## <a name="backup-to-disk-with-encryption"></a>Copia de seguridad en disco con cifrado  
 **Requisitos previos:**  
  
-   Acceso a un disco local o al almacenamiento con espacio suficiente para crear una copia de seguridad de la base de datos.  
  
-   Una clave maestra de base de datos para la base de datos maestra y un certificado o una clave asimétrica disponible en la instancia de SQL Server. Para conocer los requisitos de cifrado y los permisos, vea [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
 Siga estos pasos para crear una copia de seguridad cifrada de una base de datos en un disco local. En este ejemplo se utiliza una base de datos de usuario denominada MyTestDB.  
  
1.  **Creación de una clave maestra de base datos de la base de datos maestra:** Elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos. Conecte con el motor de base de datos, inicie una nueva ventana de consulta, copie y pegue el siguiente ejemplo y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **Creación de un certificado de copia de seguridad:** Cree un certificado de copia de seguridad en la base de datos maestra. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **Copia de seguridad de la base de datos:** Especifique el algoritmo de cifrado y el certificado que se usará. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  

    ```
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO
    ```  
  
 Para obtener un ejemplo sobre cómo cifrar una copia de seguridad protegida por EKM, vea [Administración extensible de claves con el Almacén de claves de Azure &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
### <a name="backup-to-azure-storage-with-encryption"></a>Copia de seguridad en Azure Storage con cifrado  
 Si crea una copia de seguridad en Azure Storage con la opción **SQL Server Backup to URL** (Copia de seguridad en URL de SQL Server), los pasos de cifrado son los mismos pero debe usar una dirección URL como destino y una credencial SQL para autenticarse en Azure Storage. Si quiere configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con opciones de cifrado, vea [Habilitar la copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
 **Requisitos previos:**  
  
-   Una cuenta de almacenamiento de Windows y un contenedor. Para obtener más información, vea: [Lección 1: Crear objetos de Azure Storage](https://msdn.microsoft.com/library/74edd1fd-ab00-46f7-9e29-7ba3f1a446c5).  
  
-   Una clave maestra para la base de datos maestra y un certificado o una clave asimétrica en la instancia de SQL Server. Para conocer los requisitos de cifrado y los permisos, vea [Backup Encryption](../../relational-databases/backup-restore/backup-encryption.md).  
  
1.  **Creación de una credencial de SQL Server:** Para crear una credencial de SQL Server, conéctese al motor de base de datos, abra una nueva ventana de consulta, copie y pegue el ejemplo siguiente y haga clic en **Ejecutar**.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **Cree la clave maestra de una base de datos:** Elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos. Conecte con el motor de base de datos, inicie una nueva ventana de consulta, copie y pegue el siguiente ejemplo y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **Creación de un certificado de copia de seguridad:** Cree un certificado de copia de seguridad en la base de datos maestra. Copie el ejemplo siguiente, péguelo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **Copia de seguridad de la base de datos:** Especifique el algoritmo de cifrado y el certificado que se va a usar. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' - this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  
