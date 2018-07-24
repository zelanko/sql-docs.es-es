---
title: 'PowerShell: Girar el protector del TDE: Azure SQL | Microsoft Docs'
description: Aprenda a girar el protector del Cifrado de datos transparente (TDE) de un servidor de Azure SQL.
keywords: ''
services: sql-database
documentationcenter: ''
author: becczhang
manager: jhubbard
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.tgt_pltfrm: ''
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ryzhang26
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 45dc9d4d9f4681fde06f75e8fa666c6584bcf863
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969617"
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>Girar el protector del Cifrado de datos transparente (TDE) mediante PowerShell 
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

En esta guía de procedimientos se describe la rotación de claves para un servidor de Azure SQL mediante un protector del TDE desde Azure Key Vault. La rotación del protector del TDE de un servidor de Azure SQL TDE implica cambiar a una nueva clave asimétrica que proteja las bases de datos del servidor. La rotación de claves es una operación en línea que solo debería tardar unos segundos, ya que solo descifra y vuelve a cifrar la clave de cifrado de datos de la base de datos, no toda la base de datos.

En esta guía se describen dos opciones para girar el protector del TDE en el servidor.

> [!NOTE]
> Si tiene un almacén de SQL Data Warehouse en pausa, deberá reanudarlo antes de efectuar la rotación de claves.
>

> [!IMPORTANT]
> **No elimine** las versiones anteriores de la clave después de una sustitución.  Al sustituir las claves, algunos datos siguen estando cifrados con las claves anteriores, como las copias de seguridad de base de datos antiguas. 
>

## <a name="prerequisites"></a>Prerequisites

- En esta guía de procedimientos se da por hecho que ya usa una clave de Azure Key Vault como protector de TDE para Azure SQL Database o Data Warehouse. Vea [Transparent Data Encryption with BYOK Support](transparent-data-encryption-byok-azure-sql.md) (Cifrado de datos transparente con compatibilidad para BYOK).
- Debe tener instalada y en ejecución la versión 3.7.0 o posterior de Azure PowerShell. 
- [Recomendado pero opcional] Cree el material de la clave para el protector del TDE en un módulo de seguridad de hardware (HSM) o en un almacén de claves locales y, luego, importe el material de la clave a Azure Key Vault. Siga las [instrucciones para usar un módulo de seguridad de hardware (HSM) y Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started) para obtener más información.

## <a name="option-1-auto-rotation"></a>Opción 1: Rotación automática

Genere una nueva versión de la clave del protector del TDE existente en Key Vault, con el mismo nombre de clave y el mismo almacén de claves. El servicio de SQL Azure empezará a usar esta versión nueva en un plazo de 24 horas. 

Para crear una versión del protector del TDE con el cmdlet [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey):

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>Opción 2: Rotación manual

La opción usa los cmdlets [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey), [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) y [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) para agregar una clave totalmente nueva, que podría tener un nombre nuevo o incluso otro almacén de claves. 

>[!NOTE]
>La longitud combinada del nombre del almacén de claves y del nombre de la clave no puede superar los 94 caracteres.
>

   ```powershell
   # Add a new key to Key Vault
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>

   # Add the new key from Key Vault to the server
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>   
  
   <# Set the key as the TDE protector for all resources 
   under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
  
## <a name="other-useful-powershell-cmdlets"></a>Otros cmdlets útiles de PowerShell

- Para pasar el protector del TDE del modo administrado por Microsoft al modo BYOK, use el cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector).

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- Para pasar el protector del TDE del modo BYOK al modo administrado por Microsoft, use el cmdlet [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector).

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>Pasos siguientes

- En el caso de que detecte un riesgo de seguridad, aprenda a quitar un protector del TDE que pueda estar en peligro: [Remove a potentially compromised key](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) (Quitar una clave que pueda estar en peligro) 

- Introducción a la compatibilidad de Bring Your Own Key para el TDE: [Turn on TDE using your own key from Key Vault using PowerShell](transparent-data-encryption-byok-azure-sql-configure.md) (Activar el TDE con su propia clave desde Key Vault mediante PowerShell)
