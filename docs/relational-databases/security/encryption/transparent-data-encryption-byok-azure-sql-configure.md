---
title: 'PowerShell: Habilitar el TDE con su propia clave de Azure Key Vault | Microsoft Docs'
description: "Aprenda a configurar un almacén de datos y una base de datos de Azure SQL para empezar a usar el Cifrado de datos transparente (TDE) para el cifrado en reposo mediante PowerShell."
keywords: 
documentationcenter: 
author: aliceku
manager: craigg
editor: 
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: aliceku
ms.openlocfilehash: 0acfd9faa668d1e86cb82496bdd97dc6a0ec2bc8
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="powershell-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

En esta guía de procedimientos aprenderá a usar una clave desde Azure Key Vault para el Cifrado de datos transparente (TDE) en un almacén de datos o una base de datos SQL. Para obtener más información sobre la compatibilidad del TDE con Bring Your Own Key (BYOK), vea [TDE Bring Your Own Key to Azure SQL](transparent-data-encryption-byok-azure-sql.md) (TDE con Bring Your Own Key en Azure SQL). 

## <a name="prerequisites"></a>Prerequisites

- Debe tener una suscripción de Azure y debe ser administrador en esa suscripción.
- [Recomendado pero opcional] Debería tener un módulo de seguridad de hardware (HSM) o un almacén de claves locales para crear una copia local del material de la clave del protector del TDE.
- Debe tener instalada y en ejecución la versión 4.2.0 o posterior de Azure PowerShell. 
- Debe crear un almacén de Azure Key Vault y una clave para usarlos para el TDE.
   - [Instrucciones de PowerShell de Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [Instrucciones para usar un módulo de seguridad de hardware (HSM) y Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- La clave debe tener los siguientes atributos que se usarán para el TDE:
   - Sin fecha de expiración
   - No deshabilitado
   - Debe poder llevar a cabo las operaciones *get*, *wrap key* y *unwrap key*.

## <a name="step-1-assign-an-aad-identity-to-your-server"></a>Paso 1. Asignar una identidad de AAD al servidor 

Si ya tiene un servidor, use lo siguiente para agregar una identidad de AAD al servidor:

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

Si va a crear un servidor, use el cmdlet [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) con la etiqueta -Identity para agregar una identidad de AAD durante la creación del servidor:

   ```powershell
   $server = New-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -Location <RegionName> `
   -ServerName <LogicalServerName> `
   -ServerVersion "12.0" `
   -SqlAdministratorCredentials <PSCredential> `
   -AssignIdentity 
   ```

## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>Paso 2. Conceder permisos de Key Vault al servidor

Use el cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) para conceder al servidor acceso al almacén de claves antes de usar una clave de este para el TDE.

   ```powershell
   Set-AzureRmKeyVaultAccessPolicy  `
   -VaultName <KeyVaultName> `
   -ObjectId $server.Identity.PrincipalId `
   -PermissionsToKeys get, wrapKey, unwrapKey
   ```

## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>Paso 3. Agregar la clave de Key Vault al servidor y establecer el protector del TDE

- Use el cmdlet [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) para agregar la clave de Key Vault al servidor.
- Use el cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) para establecer la clave como protector del TDE para todos los recursos del servidor.
- Use el cmdlet [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) para confirmar que el protector del TDE se ha configurado según lo previsto.

> [!Note]
> La longitud combinada del nombre del almacén de claves y del nombre de la clave no puede superar los 94 caracteres.
> 

>[!Tip]
>Id. de clave de ejemplo de Key Vault: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>

   ```powershell
   <# Add the key from Key Vault to the server #>
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>

   <# Set the key as the TDE protector for all resources under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> 

   <# To confirm that the TDE protector was configured as intended: #>
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> 
   ```

## <a name="step-4-turn-on-tde"></a>Paso 4. Activar el TDE 

Use el cmdlet [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) para activar el TDE.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `
   -State "Enabled"
   ```

Ahora, la base de datos o el almacén de datos tienen habilitado el TDE con una clave de cifrado en Key Vault.

## <a name="step-5-check-the-encryption-state-and-encryption-activity-of-the-database-or-data-warehouse"></a>Paso 5. Comprobar el estado de cifrado y la actividad de cifrado de la base de datos o del almacén de datos

Use el cmdlet [Get-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) para obtener el estado de cifrado y el cmdlet [Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) para consultar el progreso de cifrado de un almacén de datos o de una base de datos.

   ```powershell
   # Get the encryption state
   Get-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `

   <# Check the encryption progress for a database or data warehouse #>
   Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName>  
   ```

## <a name="other-useful-powershell-cmdlets"></a>Otros cmdlets útiles de PowerShell

- Use el cmdlet [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) para desactivar el TDE.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -DatabaseName <DatabaseName> `
   -State "Disabled”
   ```
 
- Use el cmdlet [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) para devolver la lista de claves de Key Vault que se han agregado al servidor.

   ```powershell
   <# KeyId is an optional parameter, to return a specific key version #>
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```
 
- Use el cmdlet [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) para quitar del servidor una clave de Key Vault.

   ```powershell
   <# The key set as the TDE Protector cannot be removed. #>
   Remove-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>   
   ```
 
## <a name="troubleshooting"></a>Solucionar problemas

Compruebe lo siguiente si se produce un problema:
- Si no se encuentra el almacén de claves, asegúrese de que está en la suscripción correcta. Para ello, use el cmdlet [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription).

   ```powershell
   Get-AzureRmSubscription `
   -SubscriptionId <SubscriptionId>
   ```

- Si la clave nueva no se puede agregar al servidor o no se puede actualizar como protector del TDE, compruebe lo siguiente:
   - La clave no debería tener ninguna fecha de expiración
   - La clave debe tener habilitadas las operaciones *get*, *wrap key* y *unwrap key*.

## <a name="next-steps"></a>Pasos siguientes

- Aprenda a girar el protector del TDE de un servidor para cumplir los requisitos de seguridad: [Girar el protector de Cifrado de datos transparente con PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md).
- En el caso de que detecte un riesgo de seguridad, aprenda a quitar un protector del TDE que pueda estar en peligro: [Remove a potentially compromised key](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) (Quitar una clave que pueda estar en peligro). 


