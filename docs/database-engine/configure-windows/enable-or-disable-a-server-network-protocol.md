---
title: Habilitar o deshabilitar un protocolo de red de servidor | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- network protocols [SQL Server], disabling
- remote connections [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], enabling using Configuration Manager
- protocols [SQL Server], disabling using Configuration Manager
- disabling network protocols, Configuration Manager
- network protocols [SQL Server], enabling
- enabling network protocols, Configuration Manager
- surface area configuration [SQL Server], connection protocols
- connections [SQL Server], enabling remote using Configuration Manager
ms.assetid: ec5ccb69-61c9-4576-8843-014b976fd46e
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: e6716392a65ce797e2f0bae543f50899b9fbeb2d
ms.contentlocale: es-es
ms.lasthandoff: 10/04/2017

---
# Habilitar o deshabilitar un protocolo de red de servidor
  Todos los protocolos de red se instalan con el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero se pueden habilitar o deshabilitar. En este tema se describe cómo habilitar o deshabilitar un protocolo de red de servidor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o PowerShell. Es preciso detener y reiniciar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que el cambio surta efecto.  
  
> [!IMPORTANT]  
>  Durante la instalación de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] se agrega un inicio de sesión para el grupo BUILTIN\Users. Esto permite que todos los usuarios autenticados del equipo tengan acceso a la instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] como un miembro del rol public. El inicio de sesión BUILTIN\Users se pueden quitar de manera segura para restringir el acceso al [!INCLUDE[ssDE](../../includes/ssde-md.md)] a los usuarios de equipos que tienen inicios de sesión individuales o son miembros de otros grupos de Windows con inicios de sesión.  
  
> [!WARNING]  
>  Los proveedores de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hasta [!INCLUDE[sssql14](../../includes/sssql14-md.md)], solo admiten TLS 1.0 y SSL 3.0 de forma predeterminada. Si aplica otro protocolo, como TLS 1.1 o TLS 1.2, al efectuar cambios en la capa SChannel del sistema operativo, es posible que las conexiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provoquen errores. Esto puede evitarse instalando la actualización adecuada para admitir TLS 1.1 y 1.2 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), que encontrará <a href="https://support.microsoft.com/en-us/help/3135244/tls-1-2-support-for-microsoft-sql-server">aquí</a>. A partir de [!INCLUDE[sssql15](../../includes/sssql15-md.md)], todas las versiones de SQL Server admiten TLS 1.2, sin necesidad de tener que aplicar ninguna otra actualización.
  
 **En este tema**  
  
-   **Para habilitar o deshabilitar un protocolo de red de servidor mediante:**  
  
     [Administrador de configuración de SQL Server](#SSMSProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### Para habilitar un protocolo de red de servidor  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en el panel de la consola, expanda **Configuración de red de SQL Server**.  
  
2.  En el panel de la consola, haga clic en **Protocolos de** *\<nombre de instancia>*.  
  
3.  En el panel de detalles, haga clic con el botón derecho en el protocolo que quiera cambiar y, después, haga clic en **Habilitar** o **Deshabilitar**.  
  
4.  En el panel de la consola, haga clic en **Servicios de SQL Server**.  
  
5.  En el panel de detalles, haga clic con el botón derecho en **SQL Server (***\<nombre de instancia>***)** y, después, haga clic en **Reiniciar** para detener y reiniciar el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="PowerShellProcedure"></a> Usar SQL Server PowerShell  
  
#### Para habilitar un protocolo de red de servidor mediante PowerShell  
  
1.  Abra un símbolo del sistema utilizando permisos de administrador.  
  
2.  Inicie Windows PowerShell desde la barra de tareas, o bien haga clic en Inicio, Todos los programas, Accesorios, Windows PowerShell y, luego, Windows PowerShell.  
  
3.  Importe el módulo **sqlps** escribiendo **Import-Module “sqlps”**.  
  
4.  Ejecute las siguientes instrucciones para habilitar los protocolos TCP y de canalizaciones con nombre. Reemplace `<computer_name>` por el nombre del equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si va a configurar una instancia con nombre, sustituya `MSSQLSERVER` por el nombre de la instancia.  
  
     Para deshabilitar los protocolos, establezca las propiedades `IsEnabled` en `$false`.  
  
    ```  
    $smo = 'Microsoft.SqlServer.Management.Smo.'  
    $wmi = new-object ($smo + 'Wmi.ManagedComputer').  
  
    # List the object properties, including the instance names.  
    $Wmi  
  
    # Enable the TCP protocol on the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    $Tcp = $wmi.GetSmoObject($uri)  
    $Tcp.IsEnabled = $true  
    $Tcp.Alter()  
    $Tcp  
  
    # Enable the named pipes protocol for the default instance.  
    $uri = "ManagedComputer[@Name='<computer_name>']/ ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Np']"  
    $Np = $wmi.GetSmoObject($uri)  
    $Np.IsEnabled = $true  
    $Np.Alter()  
    $Np  
    ```  
  
#### Para configurar los protocolos en el equipo local  
  
-   Cuando el script se ejecuta localmente y configura el equipo local, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell puede hacer que el script sea más flexible al determinar dinámicamente el nombre del equipo local. Para recuperar el nombre del equipo local, reemplace la línea donde se establece la variable `$uri` por la línea siguiente.  
  
    ```  
    $uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
    ```  
  
#### Para reiniciar el motor de base de datos mediante SQL Server PowerShell  
  
-   Después de habilitar o deshabilitar protocolos, deberá detener y reiniciar [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que se aplique el cambio. Ejecute las instrucciones siguientes para detener e iniciar la instancia predeterminada mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Para detener e iniciar una instancia con nombre, sustituya `'MSSQLSERVER'` por `'MSSQL$<instance_name>'`.  
  
    ```  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\<computer_name>  
    $Wmi = (get-item .).ManagedComputer  
    # Get a reference to the default instance of the Database Engine.  
    $DfltInstance = $Wmi.Services['MSSQLSERVER']  
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Start the service again.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache and display the state of the service.  
    $DfltInstance.Refresh(); $DfltInstance  
    ```  
  
  

