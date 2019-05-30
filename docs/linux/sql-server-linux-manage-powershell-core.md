---
title: Administrar SQL Server en Linux con PowerShell Core | Microsoft Docs
description: En este artículo se proporciona información general del uso de PowerShell Core con SQL Server en Linux.
ms.date: 04/22/2019
ms.reviewer: jroth
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: craigg
ms.openlocfilehash: 17858877efbb3f421f95b19e4b2eb66bfde5dbb4
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265343"
---
# <a name="manage-sql-server-on-linux-with-powershell-core"></a>Administrar SQL Server en Linux con PowerShell Core

Este artículo se presentan [SQL Server PowerShell](../powershell/sql-server-powershell.md) y le guía a través de un par de ejemplos acerca de cómo se usa con PowerShell Core (Core PS) en macOS y Linux. PowerShell Core ahora es un proyecto de código abierto en [GitHub](https://github.com/powershell/powershell).

## <a name="cross-platform-editor-options"></a>Opciones del editor multiplataforma

Todos los pasos siguientes de PowerShell Core funcionará en un terminal regular, o puede ejecutarlos desde un terminal en VS Code o Azure Data Studio.  VS Code y Azure Data Studio están disponibles en macOS y Linux.  Para obtener más información sobre Azure Data Studio, consulte [este inicio rápido](https://docs.microsoft.com/sql/azure-data-studio/quickstart-sql-server).  También puede considerar el uso del [extensión PowerShell](https://docs.microsoft.com/sql/azure-data-studio/powershell-extension) para él.

## <a name="installing-powershell-core"></a>Instalación de PowerShell Core

Para obtener más información acerca de cómo instalar PowerShell Core en diversas plataformas experimentales y no admitidos, consulte los artículos siguientes:

- [Instalación de PowerShell Core en Windows](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-6)
- [Instalación de PowerShell Core en Linux](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Instalación de PowerShell Core en macOS](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)
- [Instalación de PowerShell Core en ARM](https://docs.microsoft.com/powershell/scripting/install/powershell-core-on-arm?view=powershell-6)

## <a name="install-the-sqlserver-module"></a>Instale el módulo SqlServer

El `SqlServer` módulo se mantiene en el [Galería de PowerShell](https://www.powershellgallery.com/packages/SqlServer/). Cuando se trabaja con SQL Server, debe usar siempre la versión más reciente del módulo SqlServer PowerShell.

Para instalar el módulo SqlServer, abra una sesión de PowerShell Core y ejecute el siguiente código:

```powerhsell
Install-Module -Name SqlServer
```

Para obtener más información sobre cómo instalar el módulo SqlServer desde la Galería de PowerShell, consulte este [página](../powershell/download-sql-server-ps-module.md).

## <a name="using-the-sqlserver-module"></a>Con el módulo SqlServer

Comencemos por iniciar PowerShell Core.  Si se encuentra en macOS o Linux, abra un *sesión terminal* en su equipo y escriba **pwsh** para iniciar una nueva sesión de PowerShell Core.  En Windows, use <kbd>ganar</kbd>+<kbd>R</kbd>y el tipo `pwsh` para iniciar una nueva sesión de PowerShell Core.

```
pwsh
```

SQL Server proporciona un módulo de PowerShell denominado **SqlServer**. Puede usar el **SqlServer** módulo para importar los componentes de SQL Server (proveedor de SQL Server y los cmdlets) en un entorno de PowerShell o la secuencia de comandos.

Copie y pegue el siguiente comando en el símbolo del sistema de PowerShell para importar el **SqlServer** módulo en la sesión actual de PowerShell:

```powershell
Import-Module SqlServer
```

Escriba el siguiente comando en el símbolo del sistema de PowerShell para comprobar que la **SqlServer** módulo se importó correctamente:

```powershell
Get-Module -Name SqlServer
```

PowerShell debe mostrar información similar a la siguiente salida:

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## <a name="connect-to-sql-server-and-get-server-information"></a>Conectarse a SQL Server y obtener información del servidor

Los pasos siguientes utilizan PowerShell Core para conectarse a la instancia de SQL Server en Linux y mostrar un par de propiedades del servidor.

Copie y pegue los siguientes comandos en el símbolo del sistema de PowerShell. Al ejecutar estos comandos, PowerShell lo siguiente:
- Mostrar un cuadro de diálogo que le pide el nombre de host o dirección IP de la instancia
- Mostrar el *solicitud de credenciales PowerShell* cuadro de diálogo que pide las credenciales. Puede usar su *nombre de usuario SQL* y *contraseña SQL* para conectarse a la instancia de SQL Server en Linux
- Use la **Get-SqlInstance** para conectarse a la **Server** y mostrar una serie de propiedades

Si lo desea, puede reemplazar simplemente la `$serverInstance` variable con la dirección IP o el nombre de host de la instancia de SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and return a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell debe mostrar información similar a la siguiente salida:

```
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------                   -------    ------------ -----------  ------------ ----------------
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu
```

> [!NOTE]
> Si se muestra nada para estos valores, probablemente error en la conexión a la instancia de SQL Server de destino. Asegúrese de que puede usar la misma información de conexión para conectarse desde SQL Server Management Studio. Luego revise las [recomendaciones para solucionar problemas de conexión](sql-server-linux-troubleshooting-guide.md#connection).

## <a name="using-the-sql-server-powershell-provider"></a>Usar el proveedor SQL Server PowerShell

Otra opción para conectarse a la instancia de SQL Server es usar el [SQL Server PowerShell Provider](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Mediante el proveedor permite navegar por la instancia de SQL Server similar a como si se han navegar por la estructura de árbol en el Explorador de objetos, pero en la línea de comandos.  De forma predeterminada, este proveedor se presenta como un PSDrive denominado `SQLSERVER:\` que puede usar para conectar y navegar por las instancias de SQL Server que tiene acceso la cuenta de dominio.  Consulte [pasos de configuración](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) para obtener información sobre cómo configurar la autenticación de Active Directory para SQL Server en Linux.

También puede utilizar autenticación de SQL con el proveedor de PowerShell de SQL Server. Para ello, use el `New-PSDrive` para crear un PSDrive nuevo y proporcionar las credenciales adecuadas para conectarse.

En el ejemplo siguiente, verá un ejemplo de cómo crear un PSDrive nuevo mediante la autenticación de SQL.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

Puede confirmar que la unidad se creó mediante la ejecución de la `Get-PSDrive` cmdlet.

```powershell
Get-PSDrive
```

Una vez haya creado la PSDrive nuevo, puede empezar a navegar por él.

```powershell
dir SQLonDocker:\Databases
```

Este es el aspecto que podría tener la salida.  Es posible que observe esta salida es similar a lo que SSMS se mostrará en el nodo bases de datos.  Muestra las bases de datos de usuario, pero no las bases de datos del sistema.

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.57 MB Simple       140 sa
```

Si necesita ver todas las bases de datos en la instancia, una opción es usar el `Get-SqlDatabase` cmdlet.

## <a name="get-databases"></a>Obtener las bases de datos

Es un cmdlet importante conocer el `Get-SqlDatabase`.  Para muchas operaciones que implican una base de datos u objetos dentro de una base de datos, el `Get-SqlDatabase` se puede usar el cmdlet.  Si proporciona valores para ambos el `-ServerInstance` y `-Database` se recuperarán los parámetros, solo ese objeto de una base de datos.  Sin embargo, si especifica solo el `-ServerInstance` parámetro, se devolverá una lista completa de todas las bases de datos en esa instancia.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.

# Connect to the Instance and retrieve all databases
Get-SqlDatabase -ServerInstance ServerB -Credential $credential
```

Este es un ejemplo de lo que es posible que se devuelve mediante el comando Get-SqlDatabase anterior:

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2016   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2012 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2014 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2016 Normal      172.00 MB   74.88 MB Simple       130 sa
AdventureWorksDW2017 Normal      208.00 MB   40.63 MB Simple       140 sa
master               Normal        6.00 MB  600.00 KB Simple       140 sa
model                Normal       16.00 MB    5.70 MB Full         140 sa
msdb                 Normal       15.50 MB    1.14 MB Simple       140 sa
tempdb               Normal       16.00 MB    5.49 MB Simple       140 sa

```

## <a name="examine-sql-server-error-logs"></a>Examine los registros de errores de SQL Server

Los pasos siguientes utilizan PowerShell Core para examinar el error conectan los registros en la instancia de SQL Server en Linux.

Copie y pegue los siguientes comandos en el símbolo del sistema de PowerShell. Pueden tardar unos minutos en ejecutarse. Estos comandos realice los pasos siguientes:
- Mostrar un cuadro de diálogo que le pide el nombre de host o dirección IP de la instancia
- Mostrar el *solicitud de credenciales PowerShell* cuadro de diálogo que pide las credenciales. Puede usar su *nombre de usuario SQL* y *contraseña SQL* para conectarse a la instancia de SQL Server en Linux
- Use la **Get SqlErrorLog** para conectarse a la instancia de SQL Server en Linux y recuperar el error se registra desde **ayer**

Si lo desea, puede reemplazar el `$serverInstance` variable con la dirección IP o el nombre de host de la instancia de SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday
# done
```

## <a name="explore-cmdlets-currently-available-in-ps-core"></a>Explore los cmdlets disponibles actualmente en el núcleo de PS
Aunque el módulo SqlServer actualmente tiene 106 cmdlets disponibles en Windows PowerShell, 59 única de la 106 están disponibles en PSCore. A continuación, se incluye una lista completa de 59 cmdlets actualmente disponibles.  Para obtener documentación detallada de todos los cmdlets del módulo SqlServer, vea el SqlServer [referencia de cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/).

El siguiente comando mostrará todos los cmdlets disponibles en la versión de PowerShell que está usando.

```powershell
Get-Command -Module SqlServer -CommandType Cmdlet |
SORT -Property Noun |
SELECT Name
```

- ConvertFrom-EncodedSqlName
- ConvertTo-EncodedSqlName
- Get-SqlAgent
- Get-SqlAgentJob
- Get-SqlAgentJobHistory
- Get-SqlAgentJobSchedule
- Get-SqlAgentJobStep
- Get-SqlAgentSchedule
- Remove-SqlAvailabilityDatabase
- Resume-SqlAvailabilityDatabase
- Add-SqlAvailabilityDatabase
- Suspend-SqlAvailabilityDatabase
- New-SqlAvailabilityGroup
- Set-SqlAvailabilityGroup
- Remove-SqlAvailabilityGroup
- Switch-SqlAvailabilityGroup
- Join-SqlAvailabilityGroup
- Revoke-SqlAvailabilityGroupCreateAnyDatabase
- Grant-SqlAvailabilityGroupCreateAnyDatabase
- New-SqlAvailabilityGroupListener
- Set-SqlAvailabilityGroupListener
- Add-SqlAvailabilityGroupListenerStaticIp
- Set-SqlAvailabilityReplica
- Remove-SqlAvailabilityReplica
- New-SqlAvailabilityReplica
- Set-SqlAvailabilityReplicaRoleToSecondary
- New-SqlBackupEncryptionOption
- Get-SqlBackupHistory
- Invoke-Sqlcmd
- New-SqlCngColumnMasterKeySettings
- Remove-SqlColumnEncryptionKey
- Get-SqlColumnEncryptionKey
- Remove-SqlColumnEncryptionKeyValue
- Add-SqlColumnEncryptionKeyValue
- Get-SqlColumnMasterKey
- Remove-SqlColumnMasterKey
- New-SqlColumnMasterKey
- Get-SqlCredential
- Set-SqlCredential
- New-SqlCredential
- Remove-SqlCredential
- New-SqlCspColumnMasterKeySettings
- Get-SqlDatabase
- Restore-SqlDatabase
- Backup-SqlDatabase
- Set-SqlErrorLog
- Get-SqlErrorLog
- New-SqlHADREndpoint
- Set-SqlHADREndpoint
- Get-SqlInstance
- Add-SqlLogin
- Remove-SqlLogin
- Get-SqlLogin
- Set-SqlSmartAdmin
- Get-SqlSmartAdmin
- Read-SqlTableData
- Write-SqlTableData
- Read-SqlViewData
- Convert-UrnToPath

## <a name="see-also"></a>Vea también
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
