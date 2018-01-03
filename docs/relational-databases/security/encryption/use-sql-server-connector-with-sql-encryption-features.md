---
title: "Usar el Conector de SQL Server con características de cifrado de SQL | Microsoft Docs"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Connector, using
- EKM, with SQL Server Connector
ms.assetid: 58fc869e-00f1-4d7c-a49b-c0136c9add89
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e25ba8ad35a44088cee720ad626bb1524f3db1c0
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="use-sql-server-connector-with-sql-encryption-features"></a>Use SQL Server Connector with SQL Encryption Features (Usar el conector de SQL Server con características de cifrado de SQL)
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)] Las actividades de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comunes con una clave asimétrica protegida por Azure Key Vault incluyen las siguientes tres áreas:  
  
-   Cifrado de datos transparente con una clave asimétrica desde el Almacén de claves de Azure  
  
-   Cifrado de copias de seguridad con una clave asimétrica desde Key Vault  
  
-   Cifrado de nivel de columna con una clave asimétrica desde el Almacén de claves  
  
 Complete las partes de I a IV del tema [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)(Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure) antes de seguir los pasos de este tema.  
 
> [!NOTE]  
>  Las versiones 1.0.0.440 y anteriores se han reemplazado y ya no se admiten en entornos de producción. Actualice a la versión 1.0.1.0 o posterior visitando el [Centro de descargas de Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) y con las instrucciones de la sección "Actualización del conector de SQL Server" de la página [Conector de SQL Server, apéndice](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) .  
  
## <a name="transparent-data-encryption-by-using-an-asymmetric-key-from-azure-key-vault"></a>Cifrado de datos transparente con una clave asimétrica desde el Almacén de claves de Azure  
 Después de completar las partes I a IV del tema Setup Steps for Extensible Key Management Using the Azure Key Vault (Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure), use la clave del Almacén de claves de Azure para cifrar la clave de cifrado de la base de datos con TDE.  
Necesitará crear una credencial y un inicio de sesión, además de una clave de cifrado de base de datos, que cifrará los datos y registros de la base de datos. Para cifrar una base de datos, es necesario tener el permiso **CONTROL** en la base de datos. En el siguiente gráfico se muestra la jerarquía de la clave de cifrado al usar el Almacén de claves de Azure.  
  
 ![ekm&#45;key&#45;hierarchy&#45;with&#45;akv](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-with-akv.png "ekm-key-hierarchy-with-akv")  
  
1.  **Crear una credencial de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el motor de base de datos que se usará para TDE**  
  
     El motor de base de datos usa la credencial para acceder a Key Vault durante la carga de la base de datos. Se recomienda crear otro **id. de cliente** y **secreto** de Azure Active Directory en la parte I para [!INCLUDE[ssDE](../../../includes/ssde-md.md)]con el fin de limitar los permisos del Almacén de claves que se conceden.  
  
     Modifique el script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguiente como se indica a continuación:  
  
    -   Edite el argumento `IDENTITY` (`ContosoDevKeyVault`) para dirigirlo a Azure Key Vault.
        - Si usa **Azure público**, reemplace el argumento `IDENTITY` por el nombre de su Azure Key Vault de la parte II.
        - Si usa **nube pública de Azure** (por ejemplo, Azure Government, Azure China o Azure Germany), reemplace el argumento `IDENTITY` por el URI de almacén que se devolvió en la parte II, paso 3. No incluya "https://" en el URI de almacén.   
  
    -   Reemplace la primera parte del argumento `SECRET` con el **id. de cliente** de Azure de la parte I. En este ejemplo, el **id. de cliente** es `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  Debe quitar los guiones de **Client ID**.  
  
    -   Complete la segunda parte del argumento `SECRET` con el **secreto de cliente** de la parte I. En este ejemplo, el **secreto de cliente** de la parte I es `Replace-With-AAD-Client-Secret`. La cadena final para el argumento `SECRET` será una secuencia larga de letras y números, *sin guiones*.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
    ```  
  
2.  **Cree un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para TDE**  
  
     Cree un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y agréguele la credencial del Paso 1. En este ejemplo de [!INCLUDE[tsql](../../../includes/tsql-md.md)] se usa la misma clave que se importó anteriormente.  
  
    ```sql  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  **Crear la clave de cifrado de base de datos (DEK)**  
  
     La DEK cifrará los archivos de registros y datos en la instancia de la base de datos y se cifrará con la clave asimétrica del Almacén de claves de Azure. La DEK puede crearse con cualquier algoritmo compatible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y cualquier longitud de clave.  
  
    ```sql  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
    ```  
  
4.  **Activar TDE**  
  
    ```sql  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON;  
    GO  
    ```  
  
     Con [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], compruebe que se ha activado TDE conectándose a la base de datos con el Explorador de objetos. Haga clic con el botón derecho en la base de datos, seleccione **Tareas**y haga clic en **Administrar cifrado de base de datos**.  
  
     ![ekm&#45;tde&#45;object&#45;explorer](../../../relational-databases/security/encryption/media/ekm-tde-object-explorer.png "ekm-tde-object-explorer")  
  
     En el cuadro de diálogo **Administrar cifrado de base de datos** , confirme que TDE está activado y qué clave asimétrica está cifrando la DEK.  
  
     ![ekm&#45;tde&#45;dialog&#45;box](../../../relational-databases/security/encryption/media/ekm-tde-dialog-box.png "ekm-tde-dialog-box")  
  
     También puede ejecutar el siguiente script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Un estado de cifrado de 3 indica que la base de datos está cifrada.  
  
    ```sql  
    USE MASTER  
    SELECT * FROM sys.asymmetric_keys  
  
    -- Check which databases are encrypted using TDE  
    SELECT d.name, dek.encryption_state   
    FROM sys.dm_database_encryption_keys AS dek  
    JOIN sys.databases AS d  
         ON dek.database_id = d.database_id;  
    ```  
  
    > [!NOTE]  
    >  La base de datos de `tempdb` se cifra automáticamente cuando cualquier base de datos habilita TDE.  
  
## <a name="encrypting-backups-by-using-an-asymmetric-key-from-the-key-vault"></a>Cifrado de copias de seguridad con una clave asimétrica desde Key Vault  
 Las copias de seguridad cifradas se admiten a partir de [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. En el ejemplo siguiente, se crea y se restaura una copia de seguridad cifrada con una clave de cifrado de datos protegida por la clave asimétrica en el Almacén de claves.  
El [!INCLUDE[ssDE](../../../includes/ssde-md.md)] necesita las credenciales al acceder al Almacén de claves durante la carga de la base de datos. Se recomienda crear otro id. de cliente y secreto de Azure Active Directory en la parte I para el motor de base de datos con el fin de limitar los permisos que se conceden a Key Vault.  
  
1.  **Crear una credencial de SQL Server para el motor de base de datos para usar con el cifrado de copia de seguridad**  
  
     Modifique el script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguiente como se indica a continuación:  
  
    -   Edite el argumento `IDENTITY` (`ContosoDevKeyVault`) para dirigirlo a Azure Key Vault.
        - Si usa **Azure público**, reemplace el argumento `IDENTITY` por el nombre de su Azure Key Vault de la parte II.
        - Si usa **nube pública de Azure** (por ejemplo, Azure Government, Azure China o Azure Germany), reemplace el argumento `IDENTITY` por el URI de almacén que se devolvió en la parte II, paso 3. No incluya "https://" en el URI de almacén.    
  
    -   Reemplace la primera parte del argumento `SECRET` con el **id. de cliente** de Azure de la parte I. En este ejemplo, el **id. de cliente** es `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  Debe quitar los guiones de **Client ID**.  
  
    -   Complete la segunda parte del argumento `SECRET` con el **secreto de cliente** de la parte I. En este ejemplo, el **secreto de cliente** de la parte I es `Replace-With-AAD-Client-Secret`. La cadena final para el argumento `SECRET` será una secuencia larga de letras y números, *sin guiones*.   
  
        ```sql  
        USE master;  
  
        CREATE CREDENTIAL Azure_EKM_Backup_cred   
            WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
            -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
            SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;    
        ```  
  
2.  **Cree un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para el cifrado de copia de seguridad**  
  
     Cree un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que vaya a usar [!INCLUDE[ssDE](../../../includes/ssde-md.md)]para las copias de seguridad de cifrado y agréguele la credencial del Paso 1. En este ejemplo de [!INCLUDE[tsql](../../../includes/tsql-md.md)] se usa la misma clave que se importó anteriormente.  
  
    > [!IMPORTANT]  
    >  No puede usar la misma clave asimétrica para el cifrado de copias de seguridad si ya ha usado esa clave para TDE (ejemplo anterior) o el cifrado de columna (ejemplo siguiente).  
  
     En este ejemplo se usa la clave asimétrica `CONTOSO_KEY_BACKUP` almacenada en el Almacén de claves, que se puede importar o crear anteriormente para la base de datos maestra, como se describe en la Parte IV, Paso 5, más arriba.  
  
    ```sql  
    USE master;  
  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it is encrypting the backup.  
    CREATE LOGIN Backup_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY_BACKUP;  
    GO   
  
    -- Alter the Encrypted Backup Login to add the credential for use by   
    -- the Database Engine to access the key vault  
    ALTER LOGIN Backup_Login   
    ADD CREDENTIAL Azure_EKM_Backup_cred ;  
    GO  
    ```  
  
3.  **Copia de seguridad de la base de datos**  
  
     Haga una copia de seguridad de la base de datos especificando el cifrado con la clave asimétrica almacenada en Key Vault.
     
     En el ejemplo siguiente, tenga en cuenta que si la base de datos ya se ha cifrado con TDE y la clave asimétrica `CONTOSO_KEY_BACKUP` es diferente de la clave asimétrica de TDE, la copia de seguridad se cifrará tanto por la clave asimétrica TDE como por `CONTOSO_KEY_BACKUP`. La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de destino necesitará ambas claves para descifrar la copia de seguridad.
  
    ```sql  
    USE master;  
  
    BACKUP DATABASE [DATABASE_TO_BACKUP]  
    TO DISK = N'[PATH TO BACKUP FILE]'   
    WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
    ENCRYPTION(ALGORITHM = AES_256,   
    SERVER ASYMMETRIC KEY = [CONTOSO_KEY_BACKUP]);  
    GO  
    ```  
  
4.  **Restaurar la base de datos**  
    
    Para restaurar una copia de seguridad de la base de datos cifrada con TDE, la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de destino debe disponer primero de una copia de la clave asimétrica de Key Vault usada para el cifrado. Así es como se lograría:  
    
    - Si la clave asimétrica original que se usa para TDE ya no está en Key Vault, restaure la copia de seguridad de la clave de Key Vault o vuelva a importar la clave desde un HSM local. **Importante:** Para que la huella digital de la clave coincida con la huella digital registrada en la copia de seguridad de la base de datos, la clave debe tener el **mismo nombre de clave de Key Vault** que tenía originalmente.
    
    - Aplique los pasos 1 y 2 a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de destino.
    
    - Una vez que la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de destino tenga acceso a las claves asimétricas usadas para cifrar la copia de seguridad, restaure la base de datos en el servidor.
    
     Código de muestra de la restauración:  
  
    ```sql  
    RESTORE DATABASE [DATABASE_TO_BACKUP]  
    FROM DISK = N'[PATH TO BACKUP FILE]'   
        WITH FILE = 1, NOUNLOAD, REPLACE;  
    GO  
    ```  
  
     Para obtener más información sobre las opciones de copias de seguridad, vea [BACKUP (Transact-SQL)](../../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="column-level-encryption-by-using-an-asymmetric-key-from-the-key-vault"></a>Cifrado de nivel de columna con una clave asimétrica desde el Almacén de claves  
 En el ejemplo siguiente, se crea una clave simétrica protegida por la clave asimétrica en el Almacén de claves. Luego, se usa la clave simétrica para cifrar los datos de la base de datos.  
  
> [!IMPORTANT]  
>  No puede usar la misma clave asimétrica para el cifrado de copias de seguridad si ya ha usado esa clave para TDE o cifrado de copia de seguridad (ejemplos anteriores).  
  
 En este ejemplo se usa la clave asimétrica `CONTOSO_KEY_COLUMNS` almacenada en el Almacén de claves, que se puede importar o crear anteriormente, como se describe en el Paso 3, sección 3 de [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)(Pasos de instalación de Administración extensible de claves con el Almacén de claves de Azure). Para usar esta clave asimétrica en la base de datos de `ContosoDatabase` , debe ejecutar de nuevo la instrucción `CREATE ASYMMETRIC KEY` para proporcionar a la base de datos de `ContosoDatabase` una referencia a la clave.  
  
```sql  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY_COLUMNS   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoDevRSAKey2',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY_COLUMNS;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY  
    (  
    KEY_GUID('DATA_ENCRYPTION_KEY'),   
    CONVERT(VARBINARY,'Plain text data to encrypt')  
    );  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Ver también  
 [Setup Steps for Extensible Key Management Using the Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)   
 [Administración extensible de claves con el Almacén de claves de Azure](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
 [EKM provider enabled (opción de configuración del servidor)](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [Mantenimiento y solución de problemas del conector de SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  
