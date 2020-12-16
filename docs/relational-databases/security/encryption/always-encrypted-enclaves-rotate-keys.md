---
description: Rotación de claves habilitadas para el enclave
title: Rotación | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 472b37589167899314e293ff15c920bba3208962
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477556"
---
# <a name="rotate-enclave-enabled-keys"></a>Rotación de claves habilitadas para el enclave
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

En Always Encrypted, la rotación de claves es un proceso por el cual se reemplaza una clave maestra de columna existente o una clave de cifrado de columna por una clave nueva. En este artículo se describen los casos de uso y las consideraciones para la rotación de claves específica de [Always Encrypted con enclaves seguros](always-encrypted-enclaves.md) cuando la clave inicial o la clave de destino (nueva) es una clave habilitada para el enclave. Para obtener las instrucciones generales y los procesos para administrar claves de Always Encrypted, consulte [Información general de administración de claves de Always Encrypted](overview-of-key-management-for-always-encrypted.md). 

Es posible que necesite rotar una clave por motivos de seguridad o de cumplimiento. Por ejemplo, si se ha puesto en peligro una clave o las directivas de su organización requieren que reemplace las claves periódicamente. Además, Always Encrypted con la rotación de claves de enclaves seguros proporciona una manera de habilitar o deshabilitar la funcionalidad de los enclave seguros del lado servidor para las columnas cifradas.
- Cuando se reemplaza una clave que no está habilitada para el enclave con una clave habilitada para el enclave, se desbloquea la funcionalidad del enclave seguro para las consultas en una o varias columnas, protegidas con la clave. Consulte [Uso de Always Encrypted con enclaves seguros para las columnas cifradas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md).
 - Cuando se reemplaza una clave habilitada para el enclave con una clave que no está habilitada para el enclave, se deshabilita la funcionalidad del enclave seguro para las consultas en una o varias columnas, protegidas con la clave.

Si va a rotar una clave solo por motivos de seguridad o cumplimiento, y no para habilitar o deshabilitar los cálculos de enclave para las columnas, asegúrese de que la clave de destino tiene la misma configuración relativa a los enclaves que la clave de origen. Por ejemplo, si la clave de origen está habilitada para el enclave, la clave de destino también debe estarlo.

Los siguientes pasos generales incluyen vínculos a artículos detallados, en función del escenario de rotación:

1. Aprovisione una nueva clave (una clave maestra de columna o una clave de cifrado de columna).
    - Para aprovisionar una nueva clave habilitada para el enclave, consulte [Aprovisionar claves habilitadas para el enclave](always-encrypted-enclaves-provision-keys.md).
    - Para aprovisionar una clave que no está habilitada para el enclave, consulte [Aprovisionamiento de claves de Always Encrypted mediante SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md) y [Aprovisionamiento de claves de Always Encrypted con PowerShell](configure-always-encrypted-keys-using-powershell.md).
2. Reemplace una clave existente por la nueva clave.
    - Si está rotando una clave de cifrado de columna y tanto la clave de origen como la clave de destino están habilitadas para el enclave, puede ejecutar la rotación (que implica volver a cifrar los datos) en contexto. Vea [Configuración del cifrado de columnas en contexto mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-configure-encryption.md).
    - Si desea ver los pasos detallados para rotar claves, consulte [Rotación de claves de Always Encrypted mediante SQL Server Management Studio](rotate-always-encrypted-keys-using-ssms.md) y [Rotación de claves de Always Encrypted con de PowerShell](rotate-always-encrypted-keys-using-powershell.md).

    
## <a name="next-steps"></a>Pasos siguientes
- [Consulta de columnas mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Configuración del cifrado de columna en contexto mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Uso de Always Encrypted con enclaves seguros para las columnas cifradas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [Desarrollo de aplicaciones mediante Always Encrypted con enclaves seguros](always-encrypted-enclaves-client-development.md)  

## <a name="see-also"></a>Consulte también  
- [Administración de claves para Always Encrypted con enclaves seguros](always-encrypted-enclaves-manage-keys.md)

