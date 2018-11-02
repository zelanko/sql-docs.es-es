---
title: 'Configuración de TLS 1.2 en Analytics Platform System | Microsoft Docs '
description: Recomendaciones para configurar TLS 1.2 en puntos de acceso
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 638633a84721532ad05a52126aa7bcfd3f2bb6b7
ms.sourcegitcommit: 3e1efbe460723f9ca0a8f1d5a0e4a66f031875aa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2018
ms.locfileid: "50237197"
---
# <a name="configure-tls-12-in-aps"></a>Configurar TLS 1.2 en puntos de acceso

Para proteger los puntos de acceso para que solo use TLS 1.2, tendrá que deshabilitar explícitamente otro protocolo en todos los hosts físicos y virtuales. Deshabilitar protocolos requieren cambios de configuración del registro.

> [!WARNING]
> En esta sección, el método o la tarea contiene los pasos que indican cómo modificar el Registro. Sin embargo, pueden producirse problemas graves si modifica el registro incorrectamente que puede provocar la pérdida de datos y requerir la reinstalación del sistema operativo. Se recomienda encarecidamente hacer copia de seguridad del registro antes de modificarlo. A continuación, puede restaurar el Registro si se produjo un problema. Para obtener más información acerca de cómo realizar copias de seguridad y restaurar el registro, haga clic en el número de artículo siguiente para ver el artículo de Microsoft Knowledge Base:<br>
[322756](https://support.microsoft.com/en-us/help/322756) cómo realizar copias de seguridad y restaurar el registro de Windows

**Deshabilitar:**
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

También establezca las siguientes claves en el cliente de las máquinas donde se instalan las herramientas, como APS SSIS adaptadores de destino.
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```



