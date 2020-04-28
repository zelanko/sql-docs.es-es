---
title: Configuración de TLS 1,2
description: Recomendación para configurar TLS 1,2 en APS
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 988cac765a596b541d128b0b6190f6f228d95ee7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401251"
---
# <a name="configure-tls-12-in-aps"></a>Configuración de TLS 1,2 en APS

Para proteger los AP para usar solo TLS 1,2, tendrá que deshabilitar explícitamente otro protocolo en todos los hosts físicos y virtuales. La deshabilitación de los protocolos requiere cambios en la configuración del registro. Los cambios en el registro requieren un reinicio de los hosts físicos y virtuales.

> [!WARNING]
> En esta sección, el método o la tarea contiene los pasos que indican cómo modificar el Registro. Sin embargo, pueden producirse problemas graves si modifica incorrectamente el registro, lo que puede provocar la pérdida de datos y requerir la reinstalación del sistema operativo. Es muy recomendable realizar una copia de seguridad del registro antes de modificarlo. A continuación, puede restaurar el Registro si se produjo un problema. Para obtener más información acerca de cómo realizar copias de seguridad y restaurar el registro, haga clic en el número de artículo siguiente para ver el artículo en Microsoft Knowledge Base:<br>
[322756](https://support.microsoft.com/help/322756) cómo realizar una copia de seguridad y restaurar el registro en Windows

**Activa**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

Establezca también las siguientes claves en los equipos cliente donde están instaladas las herramientas como los adaptadores de destino SSIS de APS.
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



