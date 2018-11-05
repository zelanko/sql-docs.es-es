---
title: Instalar SQL Server con la configuración de estado deseado de PowerShell | Microsoft Docs
description: Aprenda a instalar SQL Server con la configuración de estado deseado (DSC) de PowerShell.
ms.custom: ''
ms.date: 10/26/2018
ms.devlang: PowerShell
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
author: randomnote1
ms.author: dareist
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 16d425d8eb66a950f432fa3ef9c68a8e68a78d22
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148487"
---
# <a name="install-sql-server-with-powershell-desired-state-configuration"></a>Instalar SQL Server con la configuración de estado deseado de PowerShell

¿Cuántas veces ha hecho clic en la interfaz de instalación de SQL Server en los mismos botones de siempre y ha escrito la misma información de siempre sin pensarlo dos veces? Luego la instalación finaliza y cae en la cuenta de que ha olvidado especificar el grupo DBA en el rol sysadmin. Ahora tiene que dedicar un tiempo precioso a ir al modo de usuario único, agregar los usuarios o grupos correctos, volver a poner SQL en modo multiusuario y probar. Lo peor es que ya se tambalea su confianza en la totalidad de la instalación. "¿Qué más he olvidado?" Yo he estado en esa situación más de una vez.

Entre en la [Configuración de estado deseado (DSC) de PowerShell](https://docs.microsoft.com/powershell/dsc/overview). Con DSC puedo crear una plantilla de configuración que se pueda volver a usar en cientos y miles de servidores. En función de la compilación, puede que tenga que ajustar algunos de los parámetros de configuración, pero eso no supone mucho, ya que puedo conservar todos los valores estándar. Lo mejor es que elimina la posibilidad de que olvide especificar un parámetro importante después de una noche sin dormir cuidando de mis hijos.

En este artículo voy a analizar la instalación inicial de una instancia independiente de SQL Server 2017 en Windows Server 2016 mediante el recurso de DSC SqlServerDsc. Le resultará útil tener conocimientos previos de DSC, ya que no voy a entrar en su funcionamiento.

Los siguientes elementos son necesarios para realizar este tutorial:

- Un equipo con Windows Server 2016
- Medios de instalación de SQL Server 2017
- El recurso de DSC SqlServerDsc (la versión 10.0.0.0 es la actual en el momento de redactar este artículo)

## <a name="prerequisites"></a>Prerequisites

En la mayoría de los casos, se usa DSC para controlar los requisitos previos, aunque para los fines de esta demostración, se van a controlar manualmente.

## <a name="install-the-sqlserverdsc-dsc-resource"></a>Instalar el recurso de DSC SqlServerDsc

El recurso de DSC [SqlServerDsc](https://www.powershellgallery.com/packages/SqlServerDsc) se puede descargar desde la [Galería de PowerShell](https://www.powershellgallery.com/) con el cmdlet [Install-Module](https://docs.microsoft.com/powershell/module/powershellget/Install-Module?view=powershell-5.1). _Nota: Asegúrese de que PowerShell se está ejecutando "Como administrador" para instalar el módulo_.

```PowerShell
Install-Module -Name SqlServerDsc
```

Obtenga los medios de instalación de SQL Server 2017. Descargue los medios de instalación de SQL Server 2017 en el servidor. Yo he descargado SQL Server 2017 Enterprise desde mi suscripción de Visual Studio y he copiado el archivo ISO en "C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso".

Ahora se debe extraer el ISO en un directorio.

```PowerShell
New-Item -Path C:\SQL2017 -ItemType Directory
$mountResult = Mount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso' -PassThru
$volumeInfo = $mountResult | Get-Volume
$driveInfo = Get-PSDrive -Name $volumeInfo.DriveLetter
Copy-Item -Path ( Join-Path -Path $driveInfo.Root -ChildPath '*' ) -Destination C:\SQL2017\ -Recurse
Dismount-DiskImage -ImagePath 'C:\en_sql_server_2017_enterprise_x64_dvd_11293666.iso'
```

## <a name="create-the-configuration"></a>Crear la configuración

### <a name="configuration"></a>Configuración

Cree la función de configuración a la que se va a llamar para generar los documentos [Managed Object Format (MOF)](https://docs.microsoft.com/windows/desktop/WmiSdk/managed-object-format--mof-).

```PowerShell
Configuration SQLInstall
{...}
```

### <a name="modules"></a>Módulos

Importe los módulos a la sesión actual. Estos módulos indican al documento de configuración cómo crear los documentos MOF y al motor de DSC cómo aplicar los documentos MOF al servidor.

```PowerShell
Import-DscResource -ModuleName SqlServerDsc
```

### <a name="resources"></a>Recursos

#### <a name="net-framework"></a>.NET Framework

SQL Server se basa en .NET Framework, por lo que es necesario asegurarse de que está instalado antes de instalar SQL Server. El recurso WindowsFeature se usa para instalar la característica de Windows Net-Framework-45-Core.

```PowerShell
WindowsFeature 'NetFramework45'
{
     Name = 'Net-Framework-45-Core'
     Ensure = 'Present'
}
```

#### <a name="sqlsetup"></a>SqlSetup

El recurso SqlSetup se usa para indicar a DSC cómo instalar SQL Server. Los parámetros necesarios para una instalación básica son:

- **InstanceName**: nombre de la instancia. Use MSSQLSERVER para una instancia predeterminada.
- **Features**: características que se van a instalar. En este ejemplo, solo voy a instalar la característica SQLEngine.
- **SourcePath**: ruta de acceso a los medios de instalación de SQL. En este ejemplo, he almacenado los medios de instalación de SQL en "C:\SQL2017". Se puede usar un recurso compartido de red para minimizar el espacio ocupado en el servidor.
- **SQLSysAdminAccounts**: usuarios o grupos que van a ser miembros del rol sysadmin. En este ejemplo, voy a conceder acceso sysadmin al grupo local Administradores. _Nota: Esta configuración no se recomienda en entornos de alta seguridad_.

Hay una lista completa y una descripción de los parámetros disponibles en SqlSetup en el [repositorio de GitHub SqlServerDsc](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlsetup).

El recurso SqlSetup es impar, porque solo instala SQL y NO conserva la configuración aplicada. Por ejemplo, si se especifica SQLSysAdminAccounts durante la instalación, un administrador puede agregar o quitar inicios de sesión en el rol sysadmin y al recurso SqlSetup no le importa. Si se quiere que DSC aplique la pertenencia del rol sysadmin, se debe usar el recurso [SqlServerRole](https://github.com/PowerShell/SqlServerDsc/tree/master#sqlserverrole).

#### <a name="complete-configuration"></a>Configuración completa

```PowerShell
Configuration SQLInstall
{
     Import-DscResource -ModuleName SqlServerDsc

     node localhost
     {
          WindowsFeature 'NetFramework45'
          {
               Name   = 'NET-Framework-45-Core'
               Ensure = 'Present'
          }

          SqlSetup 'InstallDefaultInstance'
          {
               InstanceName        = 'MSSQLSERVER'
               Features            = 'SQLENGINE'
               SourcePath          = 'C:\SQL2017'
               SQLSysAdminAccounts = @('Administrators')
               DependsOn           = '[WindowsFeature]NetFramework45'
          }
     }
}
```

## <a name="build-and-deploy"></a>Compilar e implementar

### <a name="compile-the-configuration"></a>Compilar la configuración

Use el operador punto con el script de configuración:

```PowerShell
. .\SQLInstallConfiguration.ps1
```

Ejecute la función de configuración:

```PowerShell
SQLInstall
```

En el directorio de trabajo se crea un directorio denominado "SQLInstall" que contiene una llamada de archivo "localhost.mof". Al examinar el contenido del MOF se muestra la configuración de DSC compilada.

### <a name="deploy-the-configuration"></a>Implementar la configuración

Para iniciar la implementación de DSC de SQL Server, llame al cmdlet Start-DscConfiguration. Los parámetros proporcionados al cmdlet son:

- **Path**: ruta de acceso a la carpeta que contiene los documentos MOF que se van a implementar. (Por ejemplo, "C:\SQLInstall")
- **Wait**: espera hasta que finaliza el trabajo configuración.
- **Force**: invalidación de cualquier configuración de DSC existente.
- **Verbose**: se muestra la salida detallada. Resulta útil al insertar una configuración por primera vez para ayudar a solucionar problemas.

```PowerShell
Start-DscConfiguration -Path C:\SQLInstall -Wait -Force -Verbose
```

A medida que se aplica la configuración, el resultado detallado muestra lo que sucede y da una sensación cálida y vaga de que está ocurriendo ALGO. Siempre y cuando no se produzca ningún error (texto rojo), cuando aparezca "Operation 'Invoke CimMethod' complete". en la pantalla, se debe instalar SQL.

## <a name="validate-installation"></a>Validar la instalación

### <a name="dsc"></a>DSC

Se pueden usar los cmdlets [Test-DscConfiguration](https://docs.microsoft.com/powershell/module/psdesiredstateconfiguration/test-dscconfiguration) para determinar si el estado actual del servidor, en este caso la instalación de SQL, cumple el estado deseado. El resultado de Test-DscConfiguration debe ser "True".

```PowerShell
PS C:\> Test-DscConfiguration
True
```

### <a name="services"></a>Services

La lista de servicios ahora debe devolver servicios de SQL Server

```PowerShell
PS C:\> Get-Service -Name *SQL*
Status  Name           DisplayName
------  ----           -----------
Running MSSQLSERVER    SQL Server (MSSQLSERVER)
Stopped SQLBrowser     SQL Server Browser
Running SQLSERVERAGENT SQL Server Agent (MSSQLSERVER)
Running SQLTELEMETRY   SQL Server CEIP service (MSSQLSERVER)
Running SQLWriter      SQL Server VSS Writer
```

### <a name="sql-server"></a>SQL Server

```PowerShell
PS C:\> & sqlcmd -S $env:COMPUTERNAME
1> SELECT @@SERVERNAME
2> GO
1> quit
```

## <a name="see-also"></a>Vea también

[Información general sobre la configuración de estado deseado de Windows PowerShell](https://docs.microsoft.com/powershell/dsc/overview)

[Instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)

[Instalación de SQL Server mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)
