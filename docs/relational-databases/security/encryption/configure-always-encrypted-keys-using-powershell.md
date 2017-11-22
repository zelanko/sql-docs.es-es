---
title: Configurar claves Always Encrypted con PowerShell | Microsoft Docs
ms.custom: 
ms.date: 05/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bdf8629-738c-489f-959b-2f5afdaf7d61
caps.latest.revision: "27"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e85070af106dd7f8aa334c7163fc0e1734ed86d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-always-encrypted-keys-using-powershell"></a>Configure Always Encrypted Keys using PowerShell (Configurar claves Always Encrypted con PowerShell)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

    
En este artículo se proporcionan los pasos necesarios para aprovisionar claves de Always Encrypted con el [módulo SqlServer PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md). Puede usar PowerShell para aprovisionar claves de Always Encrypted [con y sin separación de roles](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#KeyManagementRoles), lo que proporciona control sobre quién tiene acceso a las claves de cifrado reales del almacén de claves y quién tiene acceso a la base de datos. 

Para obtener información general sobre la administración de claves de Always Encrypted, incluidos algunos procedimientos recomendados de alto nivel, vea [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).
Para obtener información sobre el uso del módulo SqlServer PowerShell para Always Encrypted, vea [Configure Always Encrypted using PowerShell (Configurar Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).


## <a name="KeyProvisionWithoutRoles"></a> Aprovisionamiento de claves sin separación de roles

El método de aprovisionamiento de claves descrito en esta sección no admite la separación de roles entre Administradores de seguridad y DBA. Algunos de los pasos siguientes combinan operaciones en las claves físicas con operaciones en los metadatos de las claves. Por tanto, este método de aprovisionamiento de claves está recomendado para organizaciones que usen el modelo DevOps, o si la base de datos está hospedada en la nube y el objetivo principal es evitar que los administradores de la nube (pero no los DBA locales) accedan a información confidencial. No se recomienda si los posibles adversarios incluyen DBA o si los DBA simplemente no deben tener acceso a información confidencial.

Antes de ejecutar cualquiera de los pasos que impliquen el acceso a las claves de texto no cifrado o al almacén de claves (identificados en la columna **Accede a claves de texto no cifrado o a almacén de claves** en la tabla siguiente), asegúrese de que el entorno de PowerShell se ejecuta en un equipo seguro distinto al que hospeda la base de datos. Para obtener más información, vea ***Security Considerations for Key Management (Consideraciones de seguridad para la administración de claves)***.


Tarea  |Artículo  |Accede a claves de texto no cifrado o a almacén de claves  |Accede a base de datos   
---------|---------|---------|---------
Paso 1. Cree una clave maestra de columna en un almacén de claves.<br><br>**Nota:** El módulo SqlServer PowerShell no admite este paso. Para realizar esta tarea desde una línea de comandos, use herramientas específicas del almacén de claves seleccionado. |[Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | Sí | No     
Paso 2.  Inicie un entorno de PowerShell e importe el módulo SqlServer PowerShell.  |   [Configure Always Encrypted using PowerShell (Configurar Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   |    No    | No         
Paso 3.  Conecte con el servidor y la base de datos.     |     [Conectar con una base de datos](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase)    |    No     | Sí         
Paso 4.  Cree un objeto *SqlColumnMasterKeySettings* que contenga información sobre la ubicación de la clave maestra de columna. SqlColumnMasterKeySettings es un objeto que existe en memoria (en PowerShell). Use el cmdlet específico del almacén de claves.   |     [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)        |   No      | No         
Paso 5.  Cree los metadatos sobre la clave maestra de columna en la base de datos.      |    [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**Nota:** En segundo plano, este cmdlet emite la instrucción [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) para crear metadatos de clave.|    No     |    Sí
Paso 6.  Autentíquese en Azure si la clave maestra de columna se almacena en el Almacén de claves de Azure. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |  Sí   | No         
Paso 7.  Genere una nueva clave de cifrado de columna, cífrela con la clave maestra de columna y cree los metadatos de clave de cifrado de columna en la base de datos.     |    [New-SqlColumnEncryptionKey](https://docs.microsoft.com/en-us/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**Nota:** Use una variación del cmdlet que genera internamente y cifra una clave de cifrado de columna.<br><br>**Nota:** En segundo plano, este cmdlet emite la instrucción [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) para crear los metadatos de clave.  | Sí | Sí
  

## <a name="windows-certificate-store-without-role-separation-example"></a>Almacén de certificados de Windows sin separación de roles (ejemplo)

Este script es un ejemplo completo para generar una clave maestra de columna que sea un certificado en el Almacén de certificados de Windows, generar y cifrar una clave de cifrado de columna y crear los metadatos de clave en una base de datos de SQL Server.


```
# Create a column master key in Windows Certificate Store.
$cert1 = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert1.Thumbprint

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings


# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="azure-key-vault-without-role-separation-example"></a>Almacén de claves de Azure sin separación de roles (ejemplo)

Este script es un ejemplo completo para aprovisionar y configurar un Almacén de claves de Azure, generar una clave maestra de columna en el almacén, generar y cifrar una clave de cifrado de columna y crear los metadatos de clave en una base de datos de Azure SQL.


```
# Create a column master key in Azure Key Vault.
Login-AzureRmAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzureRMConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzureRmResourceGroup –Name $resourceGroup –Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzureRmKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzureRmKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Authenticate to Azure
Add-SqlAzureAuthenticationContext -Interactive

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="cngksp-without-role-separation-example"></a>CNG/KSP sin separación de roles (ejemplo)

El script siguiente es un ejemplo completo para generar una clave maestra de columna en un almacén de claves que implemente la API Cryptography Next Generation (CNG), generar y cifrar una clave de cifrado de columna y crear los metadatos de clave en una base de datos de SQL Server.

En el ejemplo se aprovecha el almacén de claves que usa el proveedor de almacenamiento de claves de software de Microsoft. Puede modificar el ejemplo para usar otro almacén, por ejemplo, el módulo de seguridad de hardware. Para ello, debe asegurarse de que el proveedor de almacenamiento de claves (KSP) que implementa CNG para el dispositivo esté instalado correctamente en el equipo. Debe reemplazar "Proveedor de almacenamiento de claves de software de Microsoft" por el nombre del KSP del dispositivo.


```
# Create a column master key in a key store that has a CNG provider, a.k.a key store provider (KSP).
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCngColumnMasterKeySettings -CngProviderName $cngProviderName -KeyName $cngKeyName

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="KeyProvisionWithRoles"></a> Aprovisionamiento de claves con separación de roles

En esta sección se proporcionan los pasos necesarios para configurar el cifrado cuando los administradores de seguridad no tienen acceso a la base de datos y los administradores de base de datos no tienen acceso al almacén de claves ni a las claves de texto no cifrado.


### <a name="security-administrator"></a>Administrador de seguridad

Antes de ejecutar cualquier paso que implique el acceso a las claves de texto no cifrado o al almacén de claves (identificado en la columna **Accede a claves de texto no cifrado o a almacén de claves** de la tabla siguiente), asegúrese de que:
1.  El entorno de PowerShell se ejecuta en un equipo seguro distinto al equipo que hospeda la base de datos.
2.  Los DBA de la organización no tienen acceso al equipo (eso iría contra el fin de la separación de roles).

Para obtener más información, vea [Security Considerations for Key Management (Consideraciones de seguridad para la administración de claves)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement).


Tarea  |Artículo  |Accede a claves de texto no cifrado o a almacén de claves  |Accede a base de datos  
---------|---------|---------|---------
Paso 1. Cree una clave maestra de columna en un almacén de claves.<br><br>**Nota:** El módulo SqlServer no admite este paso. Para realizar esta tarea desde una línea de comandos, debe usar herramientas específicas del tipo del almacén de claves.     | [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)  |    Sí    | No 
Paso 2.  Inicie una sesión de PowerShell e importe el módulo SqlServer.      |     [Importar el módulo SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule)     | No | No         
Paso 3.  Cree un objeto *SqlColumnMasterKeySettings* que contenga información sobre la ubicación de la clave maestra de columna. *SqlColumnMasterKeySettings* es un objeto que existe en memoria (en PowerShell). Use el cmdlet específico del almacén de claves. |      [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)   | No         | No         
Paso 4.  Autentíquese en Azure si la clave maestra de columna se almacena en el Almacén de claves de Azure. |    [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |Sí|No         
Paso 5.  Genere una clave de cifrado de columna y cífrela con la clave maestra de columna para generar un valor cifrado de la clave de cifrado de columna.     |   [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)     |    Sí    | No        
Paso 6.  Proporcione al DBA la ubicación de la clave maestra de columna (el nombre del proveedor y una ruta de acceso de la clave maestra de columna) y un valor cifrado de la clave de cifrado de columna.  | Vea los ejemplos siguientes.        |   No      | No         

### <a name="dba"></a>DBA 

Los DBA usan la información que reciben del Administrador de seguridad (paso 6 anterior) para crear y administrar los metadatos de clave de Always Encrypted en la base de datos.

Tarea  |Artículo  |Accede a claves de texto no cifrado  |Accede a base de datos   
---------|---------|---------|---------
Paso 1.  Obtenga la ubicación de la clave maestra de columna y un valor cifrado de la clave de cifrado de columna del Administrador de seguridad. |Vea los ejemplos siguientes. | No | No
Paso 2.  Inicie un entorno de PowerShell e importe el módulo SqlServer.  | [Configure Always Encrypted using PowerShell (Configurar Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)  | No | No
Paso 3.  Conecte con el servidor y una base de datos. | [Conectar con una base de datos](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | No | Sí
Paso 4.  Cree un objeto SqlColumnMasterKeySettings que contenga información sobre la ubicación de la clave maestra de columna. SqlColumnMasterKeySettings es un objeto que existe en memoria. | New-SqlColumnMasterKeySettings | No | No
Paso 5. Cree los metadatos sobre la clave maestra de columna en la base de datos. | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br>**Nota:** En segundo plano, este cmdlet emite la instrucción [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) para crear metadatos de clave maestra de columna. | No | Sí
Paso 6. Cree los metadatos de clave de cifrado de columna en la base de datos. | New-SqlColumnEncryptionKey<br>**Nota:** Los DBA usan una variación del cmdlet que solo crea los metadatos de clave de cifrado de columna.<br>En segundo plano, este cmdlet emite la instrucción [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) para crear los metadatos de clave de cifrado de columna. | No | Sí
  
## <a name="windows-certificate-store-with-role-separation-example"></a>Almacén de certificados de Windows con separación de roles (ejemplo)

### <a name="security-administrator"></a>Administrador de seguridad


```
# Create a column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Generate a column encryption key, encrypt it with the column master key to produce an encrypted value of the column encryption key.
$encryptedValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $cmkSettings

# Share the location of the column master key and an encrypted value of the column encryption key with a DBA, via a CSV file on a share drive
$keyDataFile = "Z:\keydata.txt"
"KeyStoreProviderName, KeyPath, EncryptedValue" > $keyDataFile
$cmkSettings.KeyStoreProviderName + ", " + $cmkSettings.KeyPath + ", " + $encryptedValue >> $keyDataFile

# Read the key data back to verify
$keyData = Import-Csv $keyDataFile
$keyData.KeyStoreProviderName
$keyData.KeyPath
$keyData.EncryptedValue 
```

### <a name="dba"></a>DBA

```
# Obtain the location of the column master key and the encrypted value of the column encryption key from your Security Administrator, via a CSV file on a share drive.
$keyDataFile = "Z:\keydata.txt"
$keyData = Import-Csv $keyDataFile

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $keyData.KeyStoreProviderName -KeyPath $keyData.KeyPath

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a  column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName -EncryptedValue $keyData.EncryptedValue
```  
 
## <a name="next-steps"></a>Pasos siguientes    

- [Configurar el cifrado de columna con PowerShell](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)    
- [Rotar claves de Always Encrypted con PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
    
## <a name="additional-resources"></a>Recursos adicionales    
    
- [Información general de administración de claves de Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Configurar Always Encrypted con PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted (desarrollo de clientes)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Blog de Always Encrypted](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)

