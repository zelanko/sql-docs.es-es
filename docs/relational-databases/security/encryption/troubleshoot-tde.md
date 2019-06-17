---
title: Errores comunes y soluciones con el cifrado de datos transparente (TDE) con claves administradas por el cliente en Azure Key Vault (AKV) | Microsoft Docs
description: Solucione los problemas de cifrado de datos transparente (TDE) con la configuración de Azure Key Vault.
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
ms.openlocfilehash: 1366d0a20ed39b466d1a2f6cb3e84f0f30e17f9f
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718089"
---
# <a name="common-errors-and-resolutions-with-transparent-data-encryption-tde-with-customer-managed-keys-in-azure-key-vault-akv"></a>Errores comunes y soluciones con el cifrado de datos transparente (TDE) con claves administradas por el cliente en Azure Key Vault (AKV)

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
Este tema proporciona información acerca de lo siguiente:  
  
- Requisitos  
- Cómo identificar y resolver los errores más comunes.

## <a name="requirements"></a>Requisitos
Para solucionar problemas de [TDE con el protector de TDE administrada por el cliente en la configuración de AKV](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault), vamos a empezar con la confirmación de los requisitos siguientes:
- El servidor SQL lógico y el almacén de claves se deben ubicar en la misma región.
- La identidad del servidor SQL lógico proporcionada por Azure Active Directory (APPID en Azure Key Vault) se limita a un inquilino en la suscripción original.  Si el servidor se ha movido a otra suscripción, la identidad del servidor (APPID) se tiene que volver a crear.
- El almacén de claves debe estar instalado y en ejecución, obtenga información sobre [Azure Resource Health](https://docs.microsoft.com/azure/service-health/resource-health-overview) para comprobar el estado del almacén de claves y sobre [Grupos de acciones](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups) para suscribirse a notificaciones.
- En el escenario de recuperación ante desastres con localización geográfica, con el fin de que funcionen ambos almacenes de claves, estos deben contener el mismo material de clave para una conmutación por error.
- El servidor lógico debe tener una identidad de Azure Active Directory (AAD) (APPID) para autenticarse en el almacén de claves.
- La APPID debe tener acceso al almacén de claves y al encapsulado, desencapsulado y obtención de permisos para las claves seleccionadas como protectores del TDE.

La mayoría de las incidencias detectadas al usar TDE con AKV se deben a uno de los errores de configuración siguientes:

### <a name="key-vault-unavailable-or-doesnt-exist"></a>¿El almacén de claves está deshabilitado o no existe?
- El almacén de claves se ha eliminado por error.
- El firewall se ha configurado para Azure Key Vault sin permitir el acceso a los servicios de Microsoft.

### <a name="no-permissions-to-access-the-key-vault-or-key-doesnt-exist"></a>¿No existen permisos de acceso al almacén de claves o la clave no existe?
- La clave se ha eliminado por error.
- La APPID de SQL se ha eliminado por error.
- SQL se ha movido a otra suscripción, lo que requiere una APPID nueva.
- Los permisos concedidos a la APPID para las claves no son suficientes (encapsulado, desencapsulado, obtención).
- Se han revocado los permisos para la APPID de SQL.


En la siguiente sección, vamos a enumerar los pasos para la solución de problemas de los errores más comunes.


## <a name="how-to-identify-and-resolve-the-most-common-errors"></a>Cómo identificar y resolver los errores más comunes.

## <a name="missing-server-identity"></a>Falta la auditoría de servidor.
Mensaje de error: "401 AzureKeyVaultNoServerIdentity: la identidad del servidor no se ha configurado correctamente en el servidor. Póngase en contacto con el soporte técnico".

Detección: use el siguiente comando para asegurarse de que se ha asignado una identidad al servidor SQL lógico:

- [Azure PowerShell Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 
- [CLI de Azure az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

Mitigación: configuración de una identidad de Azure Active Directory (Azure AD) (APPID) para el servidor SQL lógico.

Para PowerShell: use el comando Set-AzureRmSqlServer con la opción [- AssignIdentity](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0). 

Para la CLI: use el comando az sql server update con la opción [--assign_identity](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update). 

En Azure Portal, examine el almacén de claves y vaya a las directivas de acceso:  
 - Con el botón Agregar nuevo, agregue la APPID para el servidor que se creó en el paso anterior. 
 - Asigne los permisos de clave siguientes: obtención, encapsulado y desencapsulado. 

[Más información](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)

> [!IMPORTANT]
> Si el servidor SQL lógico se ha movido a una nueva suscripción después de la configuración inicial de TDE con AKV, el paso para configurar la identidad AAD debe repetirse con el fin de crear la APPID nueva.  Esta, después, debe agregarse al almacén de claves y se tienen que reasignar los permisos correctos. 
>

## <a name="missing-key-vault"></a>Falta el almacén de claves
Mensaje de error: "503 AzureKeyVaultConnectionFailed: la operación no ha podido completarse en el servidor debido a que se ha producido un error al intentar conectarse a Azure Key Vault".

Detección: cómo identificar el URI de clave y el almacén de claves. 

Paso 1: use el comando siguiente para obtener el URI de clave de un servidor SQL lógico determinado:

-[Azure PowerShell get-azurermsqlserverkeyvaultkey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

-[CLI de Azure az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

Paso 2: use el URI de clave para identificar el almacén de claves.

PowerShell: se pueden inspeccionar las propiedades de $MyServerKeyVaultKey para obtener detalles sobre el almacén de claves.

CLI: inspeccione el protector de cifrado de servidor devuelto para obtener más información sobre el almacén de claves.

Mitigación: confirmación de que el almacén de claves está disponible.
- Asegúrese de que el almacén de claves está disponible y el SQL Server lógico tiene acceso.
- Si el almacén de claves está protegido por un firewall, asegúrese de que está activada la casilla para permitir que los servicios de Microsoft puedan acceder al almacén de claves.
- Si el almacén de claves se ha eliminado por error, la configuración debe realizarse desde el principio.


## <a name="missing-key"></a>Falta una clave 
Mensaje de error: "404 ServerKeyNotFound: no se ha encontrado la clave de servidor solicitada en la suscripción actual".
"409 ServerKeyDoesNotExists: la clave del servidor no existe".

Detección: cómo identificar el URI de clave y el almacén de claves.
- Identifique el URI de clave agregado al servidor SQL lógico mediante los cmdlet de la sección anterior Falta el almacén de claves para devolver la lista de claves.

Mitigación: confirmación de que el protector del TDE se encuentra en AKV.
- Identifique el almacén de claves y navegue hasta él en Azure Portal.
- Asegúrese de que está la clave identificada por el URI de clave.

## <a name="missing-permissions"></a>Faltan permisos 
Mensaje de error: "401 AzureKeyVaultMissingPermissions: el servidor no encuentra los permisos necesarios en Azure Key Vault".

Detección: cómo identificar el URI de clave y el almacén de claves.
- Identifique el almacén de claves que ha usado el servidor SQL lógico mediante los cmdlet de la sección anterior Falta el almacén de claves.

Mitigación: confirmación de que el servidor SQL lógico tiene permisos para que el almacén de claves y los permisos correctos puedan acceder a la clave.
- En Azure Portal, examine el almacén de claves, vaya a las directivas de acceso y localice la APPID de SQL Server:  
  - Si la APPID no está presente, agréguela con el botón Agregar nuevo. 
  - Si la APPID está presente, asegúrese de que tiene los permisos de clave siguientes: obtención, encapsulado y desencapsulado.
