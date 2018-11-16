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
ms.openlocfilehash: 15bee3f68bf922ec9220c9ac570e5bd372f47483
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697863"
---
# <a name="configure-tls-12-in-aps"></a>Configurar TLS 1.2 en puntos de acceso

Para proteger los puntos de acceso para que solo use TLS 1.2, tendrá que deshabilitar explícitamente otro protocolo en todos los hosts físicos y virtuales. Deshabilitar protocolos requieren cambios de configuración del registro.

> [!WARNING]
> En esta sección, el método o la tarea contiene los pasos que indican cómo modificar el Registro. Sin embargo, pueden producirse problemas graves si modifica el registro incorrectamente que puede provocar la pérdida de datos y requerir la reinstalación del sistema operativo. Se recomienda encarecidamente hacer copia de seguridad del registro antes de modificarlo. A continuación, puede restaurar el Registro si se produjo un problema. Para obtener más información acerca de cómo realizar copias de seguridad y restaurar el registro, haga clic en el número de artículo siguiente para ver el artículo de Microsoft Knowledge Base:<br>
[322756](https://support.microsoft.com/help/322756) cómo realizar copias de seguridad y restaurar el registro de Windows

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



