---
title: 'Comentarios de telemetría: Analytics Platform System | Documentos de Microsoft'
description: Envíe sus comentarios de telemetría a Microsoft para Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 747274cd03e9cbd5dd2eab4423458700331358dd
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Enviar comentarios de telemetría a Microsoft para Analytics Platform System
Sistema de la plataforma de análisis tiene una característica de telemetría opcional que envía datos de la consola de administración a Microsoft. 
  
> [!NOTE]  
> En esta versión, Microsoft no se está supervisando activamente los datos de telemetría. Los datos se está recopilando solo con fines de análisis.  
  
## <a name="privacy"></a>Privacidad  
Para proporcionar la protección de la privacidad máximo, puntos de acceso se distribuye sin habilitar la telemetría. Antes de habilitar esta característica, revise la [declaración de privacidad de Microsoft Analytics Platform System](http://go.microsoft.com/fwlink/?LinkId=400902). Para dejar de participar en, ejecute la secuencia de comandos de PowerShell que se describe a continuación.  
  
## <a name="enable"></a>Habilite la telemetría  
**El reenvío de DNS:** enviar datos de telemetría a Microsoft requiere Analytics Platform System para conectarse a internet a través de un reenviador DNS. Para habilitar esta característica, debe habilitar DNS de reenvío en todos los hosts y máquinas virtuales de la carga de trabajo. Invocar la `Enable-RemoteMonitoring` comando con el `SetupDnsForwarder` opción para configurar el reenvío de DNS y habilite la telemetría correctamente. Invocar la `Enable-RemoteMonitoring` comando sin el `SetupDnsForwarder` cuando el reenvío de DNS ya está configurado y que solo desea habilitar la supervisión de latidos.  
  
> [!IMPORTANT]  
> Habilitar el reenvío de DNS, abre la conexión a internet para todos los hosts y máquinas virtuales de la carga de trabajo.  
  
#### <a name="to-enable-feedback"></a>Para habilitar los comentarios  
  
1.  Con una cuenta de administrador de dominio de aplicación, conéctese al nodo de Control (***appliance_domain *-CTL01**) y abra un símbolo del sistema con sus credenciales de administrador de Windows.  
  
2.  Navegue hasta el siguiente directorio: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importe el módulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar debe usar dos puntos en el comando.  
  
    **Ejemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invocar el `Enable-RemoteMonitoring` comando.  
  
    > [!NOTE]  
    > El script se da por supuesto que la conexión a internet funciona correctamente y no valida la conexión a internet.  
  
    1.  La primera vez que habilite la telemetría, use el comando siguiente para asegurarse de que todos los reenviadores DNS están configurados correctamente. En este ejemplo, reemplace la dirección IP de DNS reenvían `xx.xx.xx.xx` con la dirección IP del reenviador DNS en su entorno.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Cuando ya se configuran los reenviadores de DNS, como volver a habilitar deshabilitado previamente telemetría, utilice el siguiente comando para habilitar la telemetría sin configurar reenvío de DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Se le pedirá que lea y acepte que APS recopilará información sobre el dispositivo. Habrá un vínculo a la declaración de privacidad de puntos de acceso que puede copiar y pegar en cualquier explorador de internet para su revisión.  
  
6.  Escriba **Y** para aceptar y participar en comentarios o escriba **N** para no Aceptar.  
  
7.  Si escribió **Y** habrá una serie de comandos que se ejecutará, lo que le permitirá la telemetría (y, opcionalmente, el reenviador de DNS) característica en su dispositivo. Si ve errores o información que le guíe para creer que el comando no tuvo éxito póngase en contacto con CSS.  
  
Si escribió **N**, ningún comando que se va a ejecutar y no se habilitará la característica y no hay nada más para el programador.  
  
No hay peligro en cuando se ejecuta el `Enable-RemoteMonitoring` comando varias veces. Si ya se ha establecido el reenviador DNS obtendrá un mensaje de advertencia que indica que es el caso.  
  
## <a name="disable"></a>Deshabilitar la telemetría  
Deshabilitar la telemetría se detendrá todas las operaciones que se comunican información sobre el estado del dispositivo a los puntos de acceso a la supervisión de servicio en la nube.  
  
> [!IMPORTANT]  
> Llevar a cabo esta operación no se deshabilitará el reenviador de DNS o la conexión a internet que esté siendo utilizado por otras características en el dispositivo.  
  
#### <a name="to-disable-telemetry"></a>Para deshabilitar la telemetría  
  
1.  Con una cuenta de administrador de dominio de aplicación, conéctese al nodo de Control (***appliance_domain *-CTL01**) y abra una ventana de PowerShell con privilegios de administrador.  
  
2.  Navegue hasta el siguiente directorio: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importe el módulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar debe usar dos puntos en el comando.  
  
    **Ejemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invocar el `Disable-RemoteMonitoring` comando sin parámetros. Este comando dejará de enviar comentarios. (Esto no afectará la supervisión local). Sin embargo, el comando no deshabilitar el reenvío de DNS o deshabilitar cualquier conexión a internet. Esto debe hacerse manualmente después de deshabilitar correctamente los comentarios.  
  
    **Ejemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Si ve errores o información que le guíe para creer que el comando no tuvo éxito póngase en contacto con CSS.  
  
No hay peligro en cuando se ejecuta el `Disable-RemoteMonitoring` comando varias veces.  
  
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea:
- [Supervisar el dispositivo mediante la consola de administración &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Supervisar el dispositivo mediante el uso de vistas del sistema &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Supervisar el dispositivo mediante el uso de System Center Operations Manager &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Usar un reenviador DNS para resolver nombres DNS no sea de dispositivo &#40;sistema de la plataforma de análisis&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
