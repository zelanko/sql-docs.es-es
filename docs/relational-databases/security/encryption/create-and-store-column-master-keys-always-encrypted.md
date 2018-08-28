---
title: Creación y almacenamiento de claves maestras de columna (Always Encrypted) | Microsoft Docs
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 54e46ce9630ed8ae84a5998946f36d05544df34c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073746"
---
# <a name="create-and-store-column-master-keys-always-encrypted"></a>Crear y almacenar claves maestras de columna (Always Encrypted)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Las*claves maestras de columna* son claves que protegen las claves que se usan en Always Encrypted para cifrar las claves de cifrado de columnas. Las claves maestras de columna pueden almacenarse en un almacén de claves de confianza, y las claves deben ser accesibles a las aplicaciones que necesiten cifrar o descifrar datos y a las herramientas para configurar Always Encrypted y administrar las claves de Always Encrypted.

En este artículo se proporciona información para seleccionar un almacén de claves y crear claves maestras de columna para Always Encrypted. Para obtener información general detallada, vea [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

## <a name="selecting-a-key-store-for-your-column-master-key"></a>Seleccionar un almacén de claves para la clave maestra de columna

Always Encrypted admite varios almacenes de claves para almacenar las claves maestras de columna de Always Encrypted. Los almacenes de claves compatibles varían dependiendo de qué controlador y versión está usando.

Existen dos categorías de alto nivel de almacenes de claves para tener en cuenta: *Almacenes de claves locales*y *Almacenes de claves centralizados*.

###  <a name="local-or-centralized-key-store"></a>¿Almacén de claves local o centralizado?

* **Almacenes de claves locales** : solo pueden usarse por aplicaciones en equipos que contengan el almacén de claves local. En otras palabras, necesita replicar el almacén de claves y la clave en cada equipo que ejecute la aplicación. Un ejemplo de un almacén de claves local es el Almacén de certificados de Windows. Al usar un almacén de claves local, necesita asegurarse de que el almacén de claves existe en cada equipo que hospeda la aplicación y que este contiene las claves maestras de columna que la aplicación necesita para tener acceso a los datos protegidos mediante Always Encrypted. Cuando aprovisiona una clave maestra de columna por primera vez, o cuando cambia (rota) la clave, necesita asegurarse de que la clave se implementa en todos los equipos que hospedan su aplicación.

* **Almacenes de claves centralizados** : usan aplicaciones en varios equipos. Un ejemplo de un almacén de claves centralizado es el [Almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/). Un almacén de claves centralizado normalmente facilita la administración de claves porque no necesita mantener varias copias de sus claves maestras de columna en varios equipos. Necesita asegurarse de que sus aplicaciones están configuradas para conectarse al almacén de claves centralizado.

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>¿Qué almacenes de clave son compatibles en los controladores cliente habilitados para Always Encrypted?

Los controladores cliente habilitados para Always Encrypted son controladores cliente de SQL Server que tienen compatibilidad integrada para incorporar Always Encrypted en las aplicaciones cliente. Los controladores habilitados para Always Encrypted incluyen algunos proveedores integrados para los almacenes de claves conocidos. Tenga en cuenta que algunos controladores también le permiten implementar y registrar un proveedor personalizado de almacenamiento de claves maestras de columna, de forma que pueda usar cualquier almacén de claves aunque no exista un proveedor integrado para este. Al decidir entre un proveedor integrado y uno personalizado, tenga en cuenta que usar un proveedor integrado normalmente significa realizar un menor número de cambios en sus aplicaciones (en algunos casos, solo se necesita cambiar una cadena de conexión de la base de datos).

Los proveedores integrados disponibles dependen de qué controlador, qué versión de controlador y qué sistema operativo esté seleccionado.  Consulte la documentación de Always Encrypted de su controlador determinado para conocer qué almacenes de claves son compatibles de fábrica y si su controlador admite proveedores personalizados del almacén de claves.

- [Develop Applications using Always Encrypted with the .NET Framework Data Provider for SQL Server (Desarrollar aplicaciones mediante Always Encrypted con el proveedor de datos .NET Framework para SQL Server).](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


### <a name="supported-tools"></a>Herramientas compatibles

Puede usar [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) y el [módulo de SqlServer PowerShell](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update) para configurar Always Encrypted y administrar las claves de Always Encrypted. Para obtener una lista de los almacenes de claves admiten estas herramientas, vea:

- [Configure Always Encrypted using SQL Server Management Studio (Configurar Always Encrypted con SQL Server Management Studio)](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Configurar Always Encrypted con PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)


## <a name="creating-column-master-keys-in-windows-certificate-store"></a>Crear claves maestras de columna en el Almacén de certificados de Windows    

Una clave maestra de columna puede ser un certificado almacenado en el Almacén de certificados de Windows. Tenga en cuenta que un controlador habilitado para Always Encrypted no comprueba una fecha de expiración ni una cadena de entidad de certificación. Un certificado simplemente se usa como un par de claves que consta de una clave pública y una privada.

Para que una clave maestra de columna sea válida, el certificado debe:
* ser un certificado X.509.
* almacenarse en una de las dos ubicaciones de almacén de certificados: *equipo local* o *usuario actual*. (Para crear un certificado en la ubicación del almacén de certificados del equipo local, debe ser un administrador del equipo de destino).
* contener una clave privada (la longitud recomendada de las claves del certificado es de 2048 bits o superior).
* crearse para el intercambio de claves.


Existen varias maneras de crear un certificado que sea una clave maestra de columna válida pero la opción más sencilla es la de crear un certificado autofirmado.


### <a name="create-a-self-signed-certificate-using-powershell"></a>Crear un certificado autofirmado mediante PowerShell

Use el cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/library/hh848633.aspx) para crear un certificado autofirmado. En el siguiente ejemplo se muestra cómo generar un certificado que pueda usarse como una clave maestra de columna para Always Encrypted.

```
New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachine\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>Crear un certificado autofirmado mediante SQL Server Management Studio (SSMS)

Para obtener información, vea [Configure Always Encrypted using SQL Server Management Studio (Configurar Always Encrypted con SQL Server Management Studio)](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md).
Para obtener un tutorial paso a paso que usa SSMS y almacena claves Always Encrypted en el Almacén de certificados de Windows, vea [Always Encrypted: protección de los datos confidenciales en Base de datos SQL con cifrado de base de datos y almacenamiento de las claves de cifrado en el almacén de certificados de Windows](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/).


### <a name="making-certificates-available-to-applications-and-users"></a>Hacer que los certificados estén disponibles para aplicaciones y usuarios

Si la clave maestra de columna es un certificado almacenado en la ubicación del almacén de certificados del *equipo local* , necesita exportar el certificado con la clave privada e importarlo en todos los equipos que hospeden aplicaciones que está previsto que cifren o descifren datos almacenados en las columnas cifradas, o herramientas para configurar Always Encrypted y para administrar las claves Always Encrypted. Además, a cada usuario se le debe conceder un permiso de lectura para el certificado almacenado en la ubicación del almacén de certificados del equipo local para poder usar el certificado como una clave maestra de columna.

Si la clave maestra de columna es un certificado almacenado en la ubicación del almacén de certificados del *usuario actual* , necesita exportar el certificado con la clave privada e importarlo en la ubicación del almacén de certificados del usuario actual de todas las cuentas de usuario que ejecuten aplicaciones que está previsto que cifren o descifren datos almacenados en las columnas cifradas, o herramientas para configurar Always Encrypted y para administrar las claves Always Encrypted (en todos los equipos que contengan esas aplicaciones o herramientas). No se necesita ninguna configuración de permisos; después de iniciar sesión en el equipo, un usuario puede tener acceso a todos los certificados en su ubicación del almacén de certificados del usuario actual.

#### <a name="using-powershell"></a>Usar PowerShell
Use los cmdlets [Import-PfxCertificate](https://msdn.microsoft.com/library/hh848625.aspx) y [Export-PfxCertificate](https://msdn.microsoft.com/library/hh848635.aspx) para importar y exportar un certificado.

#### <a name="using-microsoft-management-console"></a>Usar Microsoft Management Console 

Para conceder al usuario el permiso de *lectura* para un certificado almacenado en la ubicación del almacén de certificados del equipo local, siga estos pasos:

1.  Abra un símbolo del sistema y escriba **mmc**.
2.  En el menú **Archivo** de la consola MMC, haga clic en **Agregar o quitar complemento**.
3.  En el cuadro de diálogo **Agregar o quitar complemento** , haga clic en **Agregar**.
4.  En el cuadro de diálogo **Agregar un complemento independiente** , haga clic en **Certificados**y, después, en **Agregar**.
5.  En el cuadro de diálogo del complemento **Certificados** , haga clic en **Cuenta de equipo**y, después, en **Finalizar**.
6.  En el cuadro de diálogo **Agregar un complemento independiente** , haga clic en **Cerrar**.
7.  En el cuadro de diálogo **Agregar o quitar complemento**, haga clic en **Aceptar**.
8.  En el complemento **Certificados**, busque el certificado en la carpeta **Certificados > Personal**, haga clic con el botón derecho en el certificado, seleccione **Todas las tareas** y, después, haga clic en **Administrar claves privadas**.
9.  En el cuadro de diálogo **Seguridad**, agregue el permiso de lectura para una cuenta de usuario si fuera necesario.

## <a name="creating-column-master-keys-in-azure-key-vault"></a>Crear claves maestras de columna en el Almacén de claves de Azure

El Almacén de claves de Azure ayuda a proteger los secretos y las claves criptográficas, y es una opción adecuada para almacenar claves maestras de columna para Always Encrypted (especialmente si sus aplicaciones se hospedan en Azure). Para crear una clave en el [Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), necesita una [suscripción de Azure](https://azure.microsoft.com/free/) y un Almacén de claves de Azure.

#### <a name="using-powershell"></a>Usar PowerShell

En el ejemplo siguiente se crea un nuevo Almacén de claves de Azure y una clave y, después, se conceden permisos para el usuario deseado.

```
# Create a column master key in Azure Key Vault.
Login-AzureRmAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzureRMContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzureRmResourceGroup –Name $resourceGroup –Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzureRmKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzureRmKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

Para obtener un tutorial paso a paso que usa SSMS y almacena claves Always Encrypted en un Almacén de claves de Azure, vea [Always Encrypted: protección de datos confidenciales en Base de datos SQL de Azure con cifrado de datos y almacenamiento de las claves de cifrado en el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault).

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>Hacer que las claves del Almacén de claves de Azure estén disponibles para aplicaciones y usuarios

Al usar una clave del Almacén de claves de Azure como una clave maestra de columna, la aplicación necesita autenticarse en Azure y la identidad de la aplicación necesita tener los siguientes permisos en el almacén de claves: *get*, *unwrapKey*y *verify*. 

Para aprovisionar claves de cifrado de columnas que se protegen con una clave maestra de columna almacenada en el Almacén de claves de Azure, necesita los permisos *get*, *unwrapKey*, *wrapKey*, *sign*y *verify* . Además, para crear una clave nueva en un Almacén de claves de Azure necesita el permiso *create* ; para enumerar los contenidos del almacén de claves necesita el permiso *list* .

#### <a name="using-powershell"></a>Usar PowerShell

Para permitir que los usuarios y las aplicaciones tengan acceso a las claves actuales del Almacén de claves de Azure, debe establecer la directiva de acceso del almacén ([Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx)):

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>Crear claves maestras de columna en módulos de seguridad de hardware con CNG

Una clave maestra de columna para Always Encrypted puede almacenarse en un almacén de claves que implemente la API de Cryptography Next Generation (CNG). Normalmente, este tipo de almacén es un módulo de seguridad de hardware (HSM). Un HSM es un dispositivo físico que protege y administra las claves digitales y proporciona un procesamiento criptográfico. Los HSM normalmente aparecen en forma de una tarjeta de complemento o un dispositivo externo que se conecta directamente a un equipo (HSM local) o a un servidor de red.

Para que un HSM esté disponible para las aplicaciones de un equipo determinado, debe instalarse y configurarse un proveedor de almacenamiento de claves (KSP), que implementa CNG, en el equipo. Un controlador cliente de Always Encrypted (un proveedor de almacenamiento de claves maestras de columna dentro del controlador) usa el KSP para cifrar y descifrar claves de cifrado de columnas, protegidas con una clave maestra de columna almacenada en el almacén de claves.

Windows incluye el proveedor de almacenamiento de claves de software de Microsoft; un KSP basado en software que puede usarse con fines de pruebas. Vea [CNG Key Storage Providers (Proveedores de almacenamiento de claves CNG)](/windows/desktop/SecCertEnroll/cng-key-storage-providers)

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>Crear claves maestras de columna en un almacén de claves mediante CNG o KSP

Una clave maestra de columna debería ser una clave asimétrica (un par con una clave pública y otra privada), mediante el algoritmo RSA. La longitud de la clave recomendada es de 2048 o superior.

#### <a name="using-hsm-specific-tools"></a>Usar herramientas específicas de HSM
Consulte la documentación de su HSM.

#### <a name="using-powershell"></a>Usar PowerShell

Puede usar las API de .NET para crear una clave en un almacén de claves con CNG en PowerShell.


```
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
```

#### <a name="using-sql-server-management-studio"></a>Usar SQL Server Management Studio

Vea [Provisioning Column Master using SQL Server Management Studio (SSMS) (Aprovisionar claves maestras de columna con SQL Server Management Studio (SSMS))](https://msdn.microsoft.com/library/mt757096.aspx#Anchor_2).


### <a name="making-cng-keys-available-to-applications-and-users"></a>Hacer que las claves CNG estén disponibles para aplicaciones y usuarios

Consulte la documentación de HSM y KSP sobre cómo configurar el KSP en un equipo y cómo conceder acceso a usuarios y aplicaciones al HSM.

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>Crear claves maestras de columna en los módulos de seguridad de hardware con CAPI

Una clave maestra de columna para Always Encrypted puede almacenarse en un almacén de claves que implemente la API de Cryptography (CAPI). Normalmente, un almacén de este tipo es un módulo de seguridad de hardware (HSM); un dispositivo físico que protege y administra las claves digitales y proporciona un procesamiento criptográfico. Los HSM normalmente aparecen en forma de una tarjeta de complemento o un dispositivo externo que se conecta directamente a un equipo (HSM local) o a un servidor de red.

Para que un HSM esté disponible para las aplicaciones de un equipo determinado, debe instalarse y configurarse un proveedor de servicios criptográficos (CSP), que implementa CAPI, en el equipo. Un controlador cliente de Always Encrypted (un proveedor de almacenamiento de claves maestras de columna dentro del controlador) usa el CSP para cifrar y descifrar claves de cifrado de columnas, protegidas con una clave maestra de columna almacenada en el almacén de claves. Nota: CAPI es una API heredada en desuso. Si hay un KSP disponible para HSM, se debe usar en lugar de un CSP o CAPI.

Un CSP debe admitir el algoritmo RSA para usarse con Always Encrypted.

Windows incluye los siguientes CSP basados en software (no están respaldados por un HSM) que admiten RSA y pueden usarse con fines de pruebas: el proveedor de servicios criptográficos RSA y AES mejorado de Microsoft.

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>Crear claves maestras de columna en un almacén de claves con CAPI o CSP

Una clave maestra de columna debería ser una clave asimétrica (un par con una clave pública y otra privada), mediante el algoritmo RSA. La longitud de la clave recomendada es de 2048 o superior.

#### <a name="using-hsm-specific-tools"></a>Usar herramientas específicas de HSM
Consulte la documentación de su HSM.

#### <a name="using-sql-server-management-studio-ssms"></a>Usar SQL Server Management Studio (SSMS)
Consulte la sección Aprovisionar claves maestras de columna en Configuring Always Encrypted using SQL Server Management Studio (Configurar Always Encrypted con SQL Server Management Studio).

 
### <a name="making-cng-keys-available-to-applications-and-users"></a>Hacer que las claves CNG estén disponibles para aplicaciones y usuarios
Consulte la documentación de HSM y CSP sobre cómo configurar el CSP en un equipo y cómo conceder acceso a usuarios y aplicaciones al HSM.
 
 
## <a name="next-steps"></a>Next Steps  
  
- [Configure Always Encrypted Keys using PowerShell (Configurar claves Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [Rotar claves de Always Encrypted con PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Configurar Always Encrypted con SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

  
## <a name="additional-resources"></a>Recursos adicionales  

- [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Develop Applications using Always Encrypted with the .NET Framework Data Provider for SQL Server (Desarrollar aplicaciones mediante Always Encrypted con el proveedor de datos .NET Framework para SQL Server)](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted Blog (Blog de Always Encrypted)](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)
    

