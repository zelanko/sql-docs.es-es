---
title: "Descarga del módulo de PowerShell de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/05/2018
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords: instalar powershell de sql server, descargar powershell de sql server
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: de203080dcc9b2c296003606e9a8067fd5dc532d
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/16/2018
---
# <a name="install-sql-server-powershell-module"></a>Instalación de un módulo de SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este artículo se proporcionan instrucciones para instalar el módulo de PowerShell **SqlServer**.

> [!NOTE]
> Hay dos módulos de SQL Server PowerShell: **SqlServer** y **SQLPS**. El módulo **SQLPS** está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**. El módulo **SqlServer** contiene versiones actualizadas de los cmdlets en **SQLPS**, así como nuevos cmdlets para admitir las características más recientes de SQL. Las versiones anteriores del módulo **SqlServer** *estaban incluidas* en SQL Server Management Studio (SSMS), pero solo con las versiones 16.x de SSMS. Para usar PowerShell con SSMS 17.0 y versiones posteriores, debe tener el módulo **SqlServer** instalado desde la Galería de PowerShell.

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

```Import-Module SqlServer -Version 21.0.17178```


Las versiones del módulo **SqlServer** de la Galería de PowerShell admiten el control de versiones y requieren la versión 5.0 de PowerShell o versiones posteriores. 

* [Módulo SqlServer en la Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver) 
* [Cmdlets de SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlets de SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
