---
title: "PowerShell - Eliminación de un protector de TDE - Azure SQL | Microsoft Docs"
description: "Guía de procedimientos para responder ante un protector de TDE que podría estar en peligro para Azure SQL Database o Data Warehouse con compatibilidad de TDE y Bring Your Own Key (BYOK)."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 861a24ef2f0bc26adece27b2612d4bf2d4640a63
ms.contentlocale: es-es
ms.lasthandoff: 09/05/2017

---


# <a name="remove-a-transparent-data-encryption-tde-protector-using-powershell"></a>Eliminación de un protector de cifrado de datos transparente (TDE) mediante PowerShell

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

## <a name="prerequisites"></a>Requisitos previos
- Debe tener una suscripción de Azure y ser administrador de esa suscripción.
- Debe tener instalada y en ejecución la versión 4.2.0 o posterior de Azure PowerShell. 
- En esta guía de procedimientos se da por hecho que ya usa una clave de Azure Key Vault como protector de TDE para Azure SQL Database o Data Warehouse. Para saber más, vea [Transparent Data Encryption with Bring Your Own Key support for Azure SQL Database and Data Warehouse](transparent-data-encryption-byok-azure-sql.md) (Cifrado de datos transparente con compatibilidad con Bring Your Own Key para Azure SQL Database y Data Warehouse).

## <a name="overview"></a>Información general
En esta guía de procedimientos se describe cómo responder ante un protector de TDE que podría estar en peligro para Azure SQL Database o Data Warehouse donde se usa TDE con compatibilidad con Bring Your Own Key (BYOK). Para obtener más información sobre la compatibilidad con BYOK para TDE, vea la [página de información general](transparent-data-encryption-byok-azure-sql.md). 

Los siguientes procedimientos deben realizarse solo en casos extremos o en entornos de prueba. Revise cuidadosamente la guía de procedimientos, ya que si elimina protectores de TDE usados activamente de Azure Key Vault podría producirse **pérdida de datos**. 

Si alguna vez se sospecha que una clave está en peligro, como por ejemplo que un servicio o un usuario han tenido acceso no autorizado a la clave, es mejor eliminar la clave.

No olvide que cuando se elimina un protector de TDE en Key Vault, **se bloquean todas las conexiones a las bases de datos cifradas en el servidor y estas bases de datos se quedan sin conexión y se quitan en un plazo de 24 horas**. Ya no se podrá acceder a las copias de seguridad antiguas que estén cifradas con la clave que está peligro.

Esta guía de procedimientos abarca dos enfoques según el resultado deseado después de la respuesta al incidente:
- Para mantener **accesibles** Azure SQL Database y SQL Data Warehouse
- Para mantener **inaccesibles** Azure SQL Database y SQL Data Warehouse

## <a name="to-keep-the-encrypted-resources-accessible"></a>Para mantener accesibles los recursos cifrados
1. Cree una [nueva clave en Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/add-azurekeyvaultkey?view=azurermps-4.1.0). Asegúrese de que esta nueva clave se crea en un almacén de claves independiente del protector de TDE potencialmente en peligro, ya que el control de acceso se aprovisiona en un nivel de almacén. 
2. Agregue la nueva clave al servidor mediante los cmdlets [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) y [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) y actualícela como el nuevo protector de TDE del servidor.

   ```powershell
   # Add the key from Key Vault to the server  
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>
   
   # Set the key as the TDE protector for all resources under the server
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault -KeyId <KeyVaultKeyId> 
   ```

3. Asegúrese de que el servidor y las réplicas se hayan actualizado al nuevo protector de TDE mediante el cmdlet [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector). 

   >[!NOTE]
   > Puede que el nuevo protector de TDE tarde unos minutos en propagarse a todas las bases de datos y bases de datos secundarias del servidor.
   >

   ```powershell
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```

4. Realice una [copia de seguridad de la nueva clave](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey) en el Key Vault.

   ```powershell
   <# -OutputFile parameter is optional; 
   if removed, a file name is automatically generated. #>
   Backup-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -OutputFile <DesiredBackupFilePath>
   ```
 
5. Elimine de Key Vault la clave en peligro mediante el cmdlet [Remove-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/remove-azurekeyvaultkey). 

   ```powershell
   Remove-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName>
   ```
 
6. Para restaurar una clave en Key Vault más adelante con el cmdlet [Restore-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey):
   ```powershell
   Restore-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -InputFile <BackupFilePath>
   ```
 
## <a name="to-make-the-encrypted-resources-inaccessible"></a>Para mantener inaccesibles los recursos cifrados
1. Quite las bases de datos que se están cifrando mediante la clave que podría estar en peligro.
Automáticamente se realiza una copia de seguridad de la base de datos y los archivos de registro, por lo que en cualquier momento puede realizarse una restauración de la base de datos a un momento dado (siempre que proporcione la clave). Las bases de datos deben quitarse antes de eliminar un protector de TDE activo para evitar hasta 10 minutos de posible pérdida de datos de las transacciones más recientes. 
2. Realice una copia de seguridad del material de clave del protector de TDE en Key Vault.
3. Quite la clave potencialmente en peligro de Key Vault.

## <a name="next-steps"></a>Pasos siguientes

- Aprenda a rotar el protector de TDE de un servidor para cumplir con los requisitos de seguridad: [Rotate the Transparent Data Encryption (TDE) protector using PowerShell](transparent-data-encryption-byok-azure-sql-key-rotation.md) (Rotación del protector de cifrado de datos transparente mediante PowerShell).

- Primeros pasos con la compatibilidad de Bring Your Own Key para TDE: [PowerShell: Enable Transparent Data Encryption using your own key from Azure Key Vault](transparent-data-encryption-byok-azure-sql-configure.md) (PowerShell: Habilitación del cifrado de datos transparente usando su propia clave de Azure Key Vault).

