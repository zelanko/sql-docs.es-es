---
title: Habilitación del protocolo TCP con SQLPS
description: Obtenga información sobre cómo habilitar los protocolos TCP mediante SQLPS.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 08/06/2020
ms.openlocfilehash: 9a3b653a0e82eed4bffdf88461474a999eef152d
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714183"
---
# <a name="how-to-enable-the-tcp-protocol"></a>Habilitación del protocolo TCP

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-with-sqlps"></a>Habilitación del protocolo TCP cuando se conecta a la consola con SQLPS

> [!Note]
> El módulo **SQLPS** está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **[SqlServer](sql-server-powershell.md)** .

1. Abra un símbolo del sistema y escriba:

    ```console
    C:\> SQLPS.EXE
    ```

    > [!TIP]
    > Si no se encuentra SQLPS, puede que necesite abrir un nuevo símbolo del sistema o cerrar sesión y volver a iniciarla.

2. En el símbolo del sistema de PowerShell, escriba:

    ```powershell
    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```

## <a name="how-to-enable-the-tcp-protocol-when-connected-to-the-console-not-using-sqlps"></a>Habilitación del protocolo TCP cuando se conecta a la consola sin usar SQLPS

1. Abra un símbolo del sistema y escriba:

    ```console
    C:\> PowerShell.exe
    ```

2. En el símbolo del sistema de PowerShell, escriba:

    ```powershell
    # Get access to SqlWmiManagement DLL on the machine with SQL
    # we are on, which is where SQL Server was installed.
    # Note: this is installed in the GAC by SQL Server Setup.

    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SqlWmiManagement')

    # Instantiate a ManagedComputer object which exposes primitives to control the
    # installation of SQL Server on this machine.

    $wmi = New-Object 'Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer' localhost

    # Enable the TCP protocol on the default instance. If the instance is named, 
    # replace MSSQLSERVER with the instance name in the following line.

    $tcp = $wmi.ServerInstances['MSSQLSERVER'].ServerProtocols['Tcp']
    $tcp.IsEnabled = $true  
    $tcp.Alter()  

    # You need to restart SQL Server for the change to persist
    # -Force takes care of any dependent services, like SQL Agent.
    # Note: if the instance is named, replace MSSQLSERVER with MSSQL$ followed by
    # the name of the instance (e.g. MSSQL$MYINSTANCE)

    Restart-Service -Name MSSQLSERVER -Force
    ```





## <a name="next-steps"></a>Pasos siguientes

- [Instalación del módulo SQL Server PowerShell](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)
- [Habilitar o deshabilitar un protocolo de red de servidor](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
- [Configurar SQL Server en una instalación Server Core](../database-engine/install-windows/configure-sql-server-on-a-server-core-installation.md)
