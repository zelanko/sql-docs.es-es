---
title: Errores comunes en el cifrado de datos transparente con claves administradas por el cliente en Azure Key Vault | Microsoft Docs
description: Solucione los problemas en el cifrado de datos transparente (TDE) con la configuración de Azure Key Vault.
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
manager: craigg
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f963e15d674115029fce78b98ba280fe75da2cd1
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716669"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Errores comunes en el cifrado de datos transparente con claves administradas por el cliente en Azure Key Vault

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
En este artículo se describen los requisitos para usar el cifrado de datos transparente (TDE) con claves administradas por el cliente en Azure Key Vault y cómo identificar y resolver los errores comunes.

## <a name="requirements"></a>Requisitos

Para solucionar problemas en el cifrado de datos transparente con un protector de TDE administrado por el usuario en Key Vault, debe cumplir con estos requisitos:

- La instancia de SQL Server lógica y el almacén de claves deben estar en la misma región.
- La identidad de la instancia de SQL Server lógica proporcionada por Azure Active Directory (Azure AD) (AppId en Azure Key Vault) debe ser un inquilino de la suscripción original. Si el servidor se movió a una suscripción distinta de donde se creó, la identidad del servidor (AppId) se debe volver a crear.
- El almacén de claves debe estar funcionando. Para saber cómo comprobar el estado del almacén de claves, consulte [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview). Si quiere registrarse para recibir notificaciones, lea sobre los [grupos de acciones](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups).
- En un escenario de recuperación ante desastres geográfica, ambos almacenes de claves deben contener el mismo material clave para que una conmutación por error funcione.
- El servidor lógico debe tener una identidad de Azure AD (AppId) para autenticarse en el almacén de claves.
- La AppId debe tener acceso al almacén de claves y debe tener los permisos Get, Wrap y Unwrap para las claves que se seleccionaron como los protectores de TDE.

Para más información, consulte [Directrices para configurar TDE con Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault).

## <a name="common-misconfigurations"></a>Configuraciones erróneas comunes

La mayoría de los problemas que se producen cuando se usa TDE con Key Vault se debe a una de las configuraciones erróneas siguientes:

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>El almacén de claves no está disponible o no existe.

- El almacén se claves se eliminó por error.
- El firewall se configuró para Azure Key Vault, pero no permite acceso a los servicios de Microsoft.

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>No existen permisos para acceder al almacén de claves o la clave no existe.

- La clave se eliminó por error.
- La AppId de la instancia de SQL Server lógica se eliminó por error.
- La instancia de SQL Server lógica se movió a otra suscripción. Se debe crear una AppId distinta si el servidor lógico se movió a otra suscripción.
- Los permisos concedidos a la AppId para las claves no son suficientes (no incluyen los permisos Get, Wrap ni Unwrap).
- Se revocaron los permisos para la AppId de la instancia de SQL Server lógica.

## <a name="identify-and-resolve-common-errors"></a>Identificación y resolución de los errores comunes

En esta sección, se muestran los pasos para resolver los errores más comunes.

### <a name="missing-server-identity"></a>Falta la auditoría de servidor.

**Mensaje de error**

_401 AzureKeyVaultNoServerIdentity: la identidad del servidor no se ha configurado correctamente en el servidor. Póngase en contacto con el soporte técnico_.

**Detección**

Use el comando o el cmdlet siguiente para asegurarse de que se asignó una identidad a la instancia de SQL Server lógica:

- Azure PowerShell: [Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- CLI de Azure: [az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**Mitigación**

Use el comando o el cmdlet siguiente para configurar una identidad de Azure AD (una AppId) para la instancia de SQL Server lógica:

- Azure PowerShell: [Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) con la opción `-AssignIdentity`.

- CLI de Azure: [az sql server update](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) con la opción `--assign_identity`.

En Azure Portal, vaya al almacén de claves y, luego, a **Directivas de acceso**. Complete estos pasos: 

 1. Use el botón **Agregar nuevo** para agregar la AppId del servidor que creó en el paso anterior. 
 1. Asigne los permisos de clave siguientes: obtención, encapsulado y desencapsulado. 

Para más información, consulte [Asignar una entidad de Azure AD al servidor](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server).

> [!IMPORTANT]
> Si la instancia de SQL Server lógica se movió a una suscripción nueva después de la configuración inicial de TDE con Key Vault, repita el paso para configurar la identidad de Azure AD y crear una nueva AppId. Luego, agregue la AppId al almacén de claves y asigne los permisos correctos a la clave. 
>

### <a name="missing-key-vault"></a>Falta el almacén de claves

**Mensaje de error**

_503 AzureKeyVaultConnectionFailed: la operación no ha podido completarse en el servidor debido a que se ha producido un error al intentar conectarse a Azure Key Vault_.

**Detección**

Para identificar un URI de clave y el almacén de claves:

1. Use el comando o el cmdlet siguiente para obtener el URI de clave de una instancia de SQL Server lógica específica:

    - Azure PowerShell: [Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - CLI de Azure: [az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. Use el URI de clave para identificar el almacén de claves:

    - Azure PowerShell: se pueden inspeccionar las propiedades de la variable $MyServerKeyVaultKey para obtener detalles sobre el almacén de claves.

    - CLI de Azure: inspeccione el protector de cifrado de servidor devuelto para obtener más información sobre el almacén de claves.

**Mitigación**

Confirme que el almacén de claves está disponible:

- Asegúrese de que el almacén de claves está disponible y de que la instancia de SQL Server lógica tiene acceso.
- Si el almacén de claves está protegido detrás de un firewall, asegúrese de que la casilla para permitir que los servicios de Microsoft pueden acceder al almacén de claves esté activada.
- Si el almacén de claves se eliminó por error, debe completar la configuración desde el inicio.


### <a name="missing-key"></a>Falta una clave

**Mensajes de error**

_404 ServerKeyNotFound: no se ha encontrado la clave de servidor solicitada en la suscripción actual_. 

_409 ServerKeyDoesNotExists: la clave del servidor no existe_.

**Detección**

Para identificar un URI de clave y el almacén de claves:

- Use el cmdlet o los comandos que aparecen en [Falta el almacén de claves](#missing-key-vault) para identificar el URI de clave que se agrega a la instancia de SQL Server lógica. La ejecución de los comandos devuelve la lista de las claves.

**Mitigación**

Confirme que el protector de TDE está presente en Key Vault:

1. Identifique el almacén de claves y vaya a él en Azure Portal.
1. Asegúrese de que está la clave identificada por el URI de clave.

### <a name="missing-permissions"></a>Faltan permisos

**Mensaje de error**

_401 AzureKeyVaultMissingPermissions: el servidor no encuentra los permisos necesarios en Azure Key Vault_.

**Detección**

Para identificar el URI de clave y el almacén de claves: 

- Use el cmdlet o los comandos que aparecen en [Falta el almacén de claves](#missing-key-vault) para identificar el almacén de claves que se usa en la instancia de SQL Server lógica.

**Mitigación**

Confirme que la instancia de SQL Server lógica tiene permisos para el almacén de claves y los permisos correctos para acceder a la clave:

- En Azure Portal, vaya al almacén de claves > **Directivas de acceso**. Busque la AppId de la instancia de SQL Server lógica.  
- Si está la AppId, asegúrese de que tiene los permisos de clave siguientes: obtención, encapsulado y desencapsulado.
- Si la AppId no está, agréguela con el botón **Agregar nuevo**. 

## <a name="next-steps"></a>Pasos siguientes

- Revise las [directrices para configurar TDE con Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault).
- Obtenga información sobre [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview).
- Obtenga una actualización de cómo [asignar una identidad de Azure AD al servidor](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server).
