---
title: Administrar SQL Server en Linux con PowerShell | Microsoft Docs
description: En este artículo se proporciona información general del uso de PowerShell en Windows con SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: a3492ce1-5d55-4505-983c-d6da8d1a94ad
ms.openlocfilehash: 8398db9e03aabf6863bd770f8be6657b58be1591
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718075"
---
# <a name="use-powershell-on-windows-to-manage-sql-server-on-linux"></a>Usar PowerShell de Windows para administrar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo se presentan [SQL Server PowerShell](../powershell/sql-server-powershell.md) y le guía a través de un par de ejemplos acerca de cómo se usa con SQL Server en Linux. Compatibilidad con PowerShell para SQL Server está actualmente disponible en Windows, MacOS y Linux. Este artículo le guiará a través del uso de una máquina de Windows para conectarse a una instancia remota de SQL Server en Linux.

## <a name="install-the-newest-version-of-sql-powershell-on-windows"></a>Instale la versión más reciente de PowerShell de SQL en Windows

[SQL PowerShell](../powershell/download-sql-server-ps-module.md) en Windows se mantiene en la Galería de PowerShell. Cuando se trabaja con SQL Server, debe usar siempre la versión más reciente del módulo SqlServer PowerShell.

## <a name="before-you-begin"></a>Antes de comenzar

Leer el [problemas conocidos](sql-server-linux-release-notes.md) para SQL Server en Linux.

## <a name="launch-powershell-and-import-the-sqlserver-module"></a>Inicie PowerShell e importe el *sqlserver* módulo

Comencemos por iniciar PowerShell en Windows. Use <kbd>ganar</kbd>+<kbd>R</kbd>, en su equipo de Windows y escriba **PowerShell** para iniciar una nueva sesión de Windows PowerShell.

```
PowerShell
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

Vamos a usar PowerShell en Windows para conectarse a la instancia de SQL Server en Linux y mostrar un par de propiedades del servidor.

Copie y pegue los siguientes comandos en el símbolo del sistema de PowerShell. Al ejecutar estos comandos, PowerShell lo siguiente:
- Mostrar un cuadro de diálogo que le pide el nombre de host o dirección IP de la instancia
- Mostrar el *solicitud de credenciales de Windows PowerShell* cuadro de diálogo que pide las credenciales. Puede usar su *nombre de usuario SQL* y *contraseña SQL* para conectarse a la instancia de SQL Server en Linux
- Use la **Get-SqlInstance** para conectarse a la **Server** y mostrar una serie de propiedades

Si lo desea, puede reemplazar simplemente la `$serverInstance` variable con la dirección IP o el nombre de host de la instancia de SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
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

Otra opción para conectarse a la instancia de SQL Server es usar el [SQL Server PowerShell Provider](https://docs.microsoft.com/sql/powershell/sql-server-powershell-provider).  Este proveedor permite navegar por la instancia de SQL Server similar a como si se han navegar por la estructura de árbol en el Explorador de objetos, pero en la línea de comandos.  De forma predeterminada, este proveedor se presenta como un PSDrive denominado `SQLSERVER:\` que puede usar para conectar y navegar por las instancias de SQL Server que tiene acceso la cuenta de dominio.  Consulte [pasos de configuración](https://docs.microsoft.com/sql/linux/sql-server-linux-active-directory-auth-overview#configuration-steps) para obtener información sobre cómo configurar la autenticación de Active Directory para SQL Server en Linux.

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

Este es el aspecto que podría tener la salida.  Es posible que observe que la salida es similar a lo que SSMS se mostrará en el nodo bases de datos.  Muestra las bases de datos de usuario, pero no las bases de datos del sistema.

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

Si necesita ver todas las bases de datos en la instancia, una opción es usar el [Get-SqlDatabase](https://docs.microsoft.com/powershell/module/sqlserver/Get-SqlDatabase) cmdlet.

## <a name="examine-sql-server-error-logs"></a>Examine los registros de errores de SQL Server

Los siguientes pasos usan PowerShell en Windows para examinar el error conectan los registros en la instancia de SQL Server en Linux. También se utilizará el **Out-GridView** cmdlet para mostrar información del error se registra en una presentación de la vista de cuadrícula.

Copie y pegue los siguientes comandos en el símbolo del sistema de PowerShell. Pueden tardar unos minutos en ejecutarse. Estos comandos realice lo siguiente:
- Mostrar un cuadro de diálogo que le pide el nombre de host o dirección IP de la instancia
- Mostrar el *solicitud de credenciales de Windows PowerShell* cuadro de diálogo que pide las credenciales. Puede usar su *nombre de usuario SQL* y *contraseña SQL* para conectarse a la instancia de SQL Server en Linux
- Use la **Get SqlErrorLog** para conectarse a la instancia de SQL Server en Linux y recuperar el error se registra desde **ayer**
- Canalizar la salida a la **Out-GridView** cmdlet

Si lo desea, puede reemplazar el `$serverInstance` variable con la dirección IP o el nombre de host de la instancia de SQL Server.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```
## <a name="see-also"></a>Vea también
- [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)
- [Cmdlets de SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
