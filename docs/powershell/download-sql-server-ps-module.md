---
title: Descarga del módulo de PowerShell de SQL Server
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: carlrab
ms.custom: ''
ms.date: 01/23/2020
ms.openlocfilehash: 99976a12ae76254da5b50c5467df9d9e42fdbbce
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "76920356"
---
# <a name="install-the-sql-server-powershell-module"></a>Instalación del módulo SQL Server PowerShell

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este artículo se proporcionan instrucciones para instalar el módulo de PowerShell **SqlServer**.

## <a name="powershell-modules-for-sql-server"></a>Módulos de PowerShell para SQL Server

Hay dos módulos de SQL Server PowerShell:

- **SqlServer**: El módulo SqlServer incluye cmdlets nuevos para la compatibilidad con las características más recientes de SQL. El módulo además contiene versiones actualizadas de los cmdlets de **SQLPS**. Para descargar el módulo SqlServer, vaya al [módulo SqlServer en la Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver).
- **SQLPS**: El módulo SQLPS está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**.

> [!NOTE]
> Las versiones del módulo **SqlServer** de la Galería de PowerShell admiten el control de versiones y requieren la versión 5.0 de PowerShell o versiones posteriores.

Para ver los temas de ayuda, vaya a:

- Cmdlets de [SqlServer](https://docs.microsoft.com/powershell/module/sqlserver).
- Cmdlets de [SQLPS](https://docs.microsoft.com/powershell/module/sqlps).

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

SQL Server Management Studio (SSMS), a partir de la versión 17.0, no instala ninguno de los módulos de PowerShell. Para usar PowerShell con SSMS, instale el módulo **SqlServer** desde la [Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver).

> [!NOTE]
> Con la versión 16. x de SSMS, se incluye una versión anterior del módulo **SqlServer** con SQL Server Management Studio (SSMS).

## <a name="azure-data-studio"></a>Azure Data Studio

Azure Data Studio no instala ninguno de los módulos de PowerShell. Para usar PowerShell con Azure Data Studio, instale el módulo **SqlServer** desde la [Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver).

Puede usar la [extensión de PowerShell](../azure-data-studio/powershell-extension.md) que proporciona compatibilidad con el editor de PowerShell enriquecida en Azure Data Studio.

## <a name="installing-or-updating-the-sqlserver-module"></a>Instalación o actualización del módulo SqlServer

Para instalar el módulo **SqlServer** desde la Galería de PowerShell, inicie una sesión de [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) como administrador. También puede iniciar Azure Data Studio como administrador y ejecutar estos comandos en una sesión de PowerShell en el terminal integrado.

### <a name="install-the-sqlserver-module"></a>Instalación del módulo SqlServer

Ejecute el comando siguiente en la sesión de PowerShell para instalar el módulo SqlServer para todos los usuarios:

```powershell
Install-Module -Name SqlServer
```

### <a name="to-view-the-versions-of-the-sqlserver-module-installed"></a>Para ver las versiones del módulo SqlServer instaladas

Ejecute el comando siguiente para ver las versiones del módulo SqlServer que se han instalado.

```powershell
Get-Module SqlServer -ListAvailable
```

### <a name="install-for-the-current-user-rather-than-as-an-administrator"></a>Instalación para el usuario actual en lugar de como administrador

Si no puede ejecutar la sesión de PowerShell como administrador, haga la instalación para el usuario actual con el comando siguiente:

```powershell
Install-Module -Name SqlServer -Scope CurrentUser
```

### <a name="to-overwrite-a-previous-version-of-the-sqlserver-module"></a>Para sobrescribir una versión anterior del módulo SqlServer

También puede usar el comando `Install-Module` para sobrescribir una versión anterior.

```powershell
Install-Module -Name SqlServer -AllowClobber
```

> [!Note]
> PowerShell siempre usa el módulo más reciente instalado.

### <a name="update-the-installed-version-of-the-sqlserver-module"></a>Actualización de la versión instalada del módulo SqlServer

Cuando haya disponibles versiones actualizadas del módulo **SqlServer**, puede instalar la versión más reciente con el comando siguiente:

```powershell
Install-Module -Name SqlServer -AllowClobber
```

Puede usar el comando `Update-Module` para instalar la versión más reciente del módulo SQLServer de PowerShell, pero eso no quita las versiones anteriores. Instala la versión más reciente en paralelo para que pueda experimentar con la versión más reciente, pero con los módulos más antiguos todavía instalados.

Sin embargo, si no quiere conservar las versiones anteriores del módulo, puede usar el comando `Uninstall-Module` para quitarlas.

Puede usar el comando siguiente para enumerar si hay más de una versión instalada:

```powershell
Get-Module SqlServer -ListAvailable
```

Puede usar el comando siguiente para quitar versiones anteriores:

```powershell
Uninstall-module -Name SQLServer -RequiredVersion "<version number>" -AllowClobber
```

### <a name="troubleshooting"></a>Solución de problemas

Si le surgen problemas durante la instalación, consulte la [documentación de instalación de módulos](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1) y la [referencia de instalación de módulos](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

## <a name="using-a-specific-version-of-the-sqlserver-module"></a>Uso de una versión específica del módulo SqlServer

Para usar una versión específica del módulo, impórtela con un número de versión específico de forma similar al comando siguiente:

```powershell
Import-Module SqlServer -Version 21.1.18080
```

## <a name="pre-release-versions-of-the-sqlserver-module"></a>Versiones preliminares del módulo SqlServer

Las versiones preliminares del módulo SqlServer pueden estar disponibles en la Galería de PowerShell.

> [!IMPORTANT]
> Estas versiones se pueden detectar e instalar mediante los cmdlets actualizados *Find-Module* e *Install-Module* que forman parte del módulo [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) si se pasa el modificador *-AllowPrerelease*. Para usar estos cmdlets, instale el módulo PowerShellGet y, a continuación, abra una sesión nueva.

### <a name="to-discover-pre-release-versions-of-the-sqlserver-module"></a>Para detectar las versiones preliminares del módulo SqlServer

Para detectar las versiones preliminares del módulo SqlServer, ejecute el comando siguiente:

```powershell
Find-Module SqlServer -AllowPrerelease
```

### <a name="to-install-a-specific-pre-release-version-of-the-sqlserver-module"></a>Para instalar una versión preliminar específica del módulo SqlServer

Para instalar una versión de lanzamiento preliminar específica del módulo, instálela con un número de versión específico.

Puede intentar usar el comando siguiente:

```powershell
Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease
```

## <a name="sql-server-powershell-on-linux"></a>SQL Server PowerShell en Linux

Visite [Administración de SQL Server en Linux con PowerShell Core](../linux/sql-server-linux-manage-powershell-core.md) para ver cómo instalar SQL Server PowerShell en Linux.
