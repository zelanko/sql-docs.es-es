---
title: Descarga del módulo de PowerShell de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- instalar powershell de sql server, descargar powershell de sql server
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0f14a3cee050fff07c7fe5bc2467bcb8209a53c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672571"
---
# <a name="install-sql-server-powershell-module"></a>Instalación de un módulo de SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este artículo se proporcionan instrucciones para instalar el módulo de PowerShell **SqlServer**.
> [!NOTE]
> Hay dos módulos de SQL Server PowerShell: 
> * **SQLPS**: este módulo se incluye en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**.
> * **SqlServer**: en este módulo, se incluyen nuevos cmdlets para la compatibilidad con las características más recientes de SQL. El módulo además contiene versiones actualizadas de los cmdlets de **SQLPS**. 

Las versiones anteriores del módulo **SqlServer** *estaban incluidas* en SQL Server Management Studio (SSMS), pero solo con las versiones 16.x de SSMS. Para usar PowerShell con SSMS 17.0 y versiones posteriores, debe tener el módulo **SqlServer** instalado desde la [Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver).
La versión actual del módulo **SqlServer** es 21.1.18080. Se basa en la versión 150 de Microsoft.SQLServer.SMO y admite la próxima versión de SQL Server. La versión más reciente del módulo basada en la versión 140 de Microsoft.SQLServer.SMO es 21.0.17279.

Las versiones preliminares del módulo pueden estar disponibles con mayor frecuencia: vea la sección al final de esta página para obtener información sobre cómo descargar esas versiones del módulo.

Para instalar el módulo **SqlServer** desde la Galería de PowerShell, inicie una sesión de [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) y use los siguientes comandos. Si le surgen problemas durante la instalación, consulte la [documentación de instalación de módulos](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module) y la [referencia de instalación de módulos](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

Para instalar el módulo **SqlServer**:

```Install-Module -Name SqlServer```

Si tiene versiones anteriores del módulo **SqlServer** en el equipo, es posible que pueda usar `Update-Module` (más adelante en este artículo) o proporcionar el parámetro `-AllowClobber`:  

```Install-Module -Name SqlServer -AllowClobber```

Si no puede ejecutar la sesión de PowerShell como administrador, puede instalar el módulo para el usuario actual:

```Install-Module -Name SqlServer -Scope CurrentUser```

Cuando estén disponibles nuevas versiones del módulo **SqlServer**, puede actualizarlas con `Update-Module`:

```Update-Module -Name SqlServer```

Para ver las versiones del módulo instaladas:

```Get-Module SqlServer -ListAvailable```

Para usar una versión específica del módulo, puede importarla con un número de versión específico de forma similar a la siguiente:

```Import-Module SqlServer -Version 21.1.18080```

> [!NOTE]
> Las versiones preliminares del módulo pueden estar disponibles en la Galería de PowerShell. Se pueden detectar e instalar mediante los cmdlets actualizados *Find-Module* e *Install-Module* que forman parte del módulo [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) si se pasa el modificador *-AllowPrerelease*.
>
> Para detectar la versión preliminar del módulo, puede ejecutar el comando siguiente:
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> Para instalar una versión preliminar concreta del módulo, puede hacerlo con un número de versión específico de forma similar a la siguiente:
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

Las versiones del módulo **SqlServer** de la Galería de PowerShell admiten el control de versiones y requieren la versión 5.0 de PowerShell o versiones posteriores. 

* [Módulo SqlServer en la Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver) 
* [Cmdlets de SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlets de SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
