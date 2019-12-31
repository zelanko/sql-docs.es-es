---
title: Comentarios sobre telemetría
description: Envíe comentarios de telemetría a Microsoft for Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 639eb4e9e5c531e154b9eb7f91165af365bc519f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400359"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Enviar comentarios de telemetría a Microsoft for Analytics Platform System
Analytics Platform System tiene una característica de telemetría opcional que envía datos de la consola de administración a Microsoft. 
  
> [!NOTE]  
> En esta versión, Microsoft no está supervisando activamente los datos de telemetría. Los datos se recopilan solo con fines de análisis.  
  
## <a name="privacy"></a>Service  
Para proporcionar la máxima protección de privacidad, APS se suministra sin habilitar la telemetría. Antes de habilitar esta característica, revise primero la [Microsoft Analytics Platform System declaración de privacidad](https://go.microsoft.com/fwlink/?LinkId=400902). Para participar, ejecute el script de PowerShell que se describe a continuación.  
  
## <a name="enable"></a>Habilitar la telemetría  
**Reenvío de DNS:** El envío de datos de telemetría a Microsoft requiere Analytics Platform System para conectarse a Internet a través de un reenviador de DNS. Para habilitar esta característica, debe habilitar el reenvío de DNS en todos los hosts y máquinas virtuales de carga de trabajo. Invoque `Enable-RemoteMonitoring` el comando con `SetupDnsForwarder` la opción de configurar correctamente el reenvío de DNS y habilitar la telemetría. Invoque `Enable-RemoteMonitoring` el comando sin `SetupDnsForwarder` la opción cuando el reenvío de DNS ya esté configurado y solo desee habilitar la supervisión de latidos.  
  
> [!IMPORTANT]  
> Al habilitar el reenvío DNS, se abre la conexión a Internet para todos los hosts y máquinas virtuales de carga de trabajo.  
  
#### <a name="to-enable-feedback"></a>Para habilitar los comentarios  
  
1.  Mediante una cuenta de administrador de dominio de dispositivo, conéctese al nodo de control (<strong>*appliance_domain*-CTL01</strong>) y abra un símbolo del sistema con las credenciales de administrador de Windows.  
  
2.  Navegue hasta el siguiente directorio: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importar el módulo`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar, debe usar dos puntos en el comando.  
  
    **Ejemplo**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invoque `Enable-RemoteMonitoring` el comando.  
  
    > [!NOTE]  
    > El script supone que la conexión a Internet funciona correctamente y no valida la conexión a Internet.  
  
    1.  La primera vez que habilite la telemetría, use el siguiente comando para asegurarse de que todos los reenviadores DNS estén configurados correctamente. En este ejemplo, reemplace la dirección `xx.xx.xx.xx` IP reenviada DNS por la dirección IP del reenviador DNS de su entorno.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Cuando ya estén configurados los reenviadores de DNS, como volver a habilitar la telemetría previamente deshabilitada, use el siguiente comando para habilitar la telemetría sin configurar el reenvío de DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Se le pedirá que lea y confirme que APS recopilará información sobre el dispositivo. Habrá un vínculo a la declaración de privacidad del APS que puede copiar y pegar en cualquier explorador de Internet para su revisión.  
  
6.  Escriba **y** para aceptar y participar en los comentarios o escriba **N** para no aceptar.  
  
7.  Si ha escrito **Y** , habrá una serie de comandos que se ejecutarán, lo que habilitará la característica de telemetría (y, opcionalmente, el reenviador DNS) en el dispositivo. Si ve algún error o información que le lleve a creer que el comando no se ha realizado correctamente, póngase en contacto con CSS para obtener ayuda.  
  
Si ha escrito **N**, no se ejecutará ningún comando y la característica no estará habilitada y no habrá nada más que hacer.  
  
No hay ningún daño en ejecutar el `Enable-RemoteMonitoring` comando varias veces. Si el reenviador DNS ya está establecido, recibirá un mensaje de advertencia que indica que es el caso.  
  
## <a name="disable"></a>Deshabilitar la telemetría  
Al deshabilitar la telemetría, se detendrán todas las operaciones que comunican información sobre el estado del dispositivo al servicio de supervisión de APS en la nube.  
  
> [!IMPORTANT]  
> Al realizar esta operación, no se deshabilitará el reenviador DNS o la conexión a Internet que otras características del dispositivo pueden usar.  
  
#### <a name="to-disable-telemetry"></a>Para deshabilitar la telemetría  
  
1.  Con una cuenta de administrador de dominio de dispositivo, conéctese al nodo de control (<strong>*appliance_domain*-CTL01</strong>) y abra una ventana de PowerShell con privilegios de administrador.  
  
2.  Navegue hasta el siguiente directorio: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importar el módulo`Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar, debe usar dos puntos en el comando.  
  
    **Ejemplo**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invoque `Disable-RemoteMonitoring` el comando sin parámetros. Este comando dejará de enviar comentarios. (Esto no afectará a la supervisión local). Sin embargo, el comando no deshabilitará el reenviador de DNS ni deshabilitar la conectividad a Internet. Esto debe realizarse manualmente después de deshabilitar correctamente los comentarios.  
  
    **Ejemplo**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Si ve algún error o información que le lleve a creer que el comando no se ha realizado correctamente, póngase en contacto con CSS para obtener ayuda.  
  
No hay ningún daño en ejecutar el `Disable-RemoteMonitoring` comando varias veces.  
  
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, consulte:
- [Supervise el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Supervise el dispositivo mediante las vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Supervise el dispositivo mediante System Center Operations Manager &#40;de sistema de plataforma de análisis&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Usar un reenviador DNS para resolver nombres DNS que no sean de aplicación &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
