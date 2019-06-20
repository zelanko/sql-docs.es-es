---
title: Comentarios de telemetría - Analytics Platform System | Microsoft Docs
description: Enviar comentarios de telemetría a Microsoft para Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 442505d470d1c7b7a82a02610d650d9f0b8c8d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678376"
---
# <a name="send-telemetry-feedback-to-microsoft-for-analytics-platform-system"></a>Enviar comentarios de telemetría a Microsoft para Analytics Platform System
Analytics Platform System tiene una característica opcional de telemetría que envía datos de la consola de administración a Microsoft. 
  
> [!NOTE]  
> En esta versión, Microsoft no supervisa activamente los datos de telemetría. Los datos se recopilan solo con fines de análisis.  
  
## <a name="privacy"></a>Privacidad  
Para proporcionar la protección de privacidad máximo, puntos de acceso se incluye sin habilitar la telemetría. Antes de habilitar esta característica, revise el [declaración de privacidad de Microsoft Analytics Platform System](https://go.microsoft.com/fwlink/?LinkId=400902). Para participar en, ejecute el script de PowerShell que se describe a continuación.  
  
## <a name="enable"></a>Habilitar la telemetría  
**Reenvío de DNS:** Requiere que envían datos de telemetría a Microsoft Analytics Platform System para conectarse a internet a través de un reenviador DNS. Para habilitar esta característica, debe habilitar en todos los hosts y máquinas virtuales de carga de trabajo de reenvío de DNS. Invocar el `Enable-RemoteMonitoring` comando con el `SetupDnsForwarder` opción para configurar el reenvío de DNS y habilitar la telemetría correctamente. Invocar el `Enable-RemoteMonitoring` comando sin el `SetupDnsForwarder` opción cuando el reenvío de DNS ya está configurado y desea habilitar la supervisión de latido.  
  
> [!IMPORTANT]  
> Habilitar el reenvío de DNS, abre la conexión a internet para todos los hosts y máquinas virtuales de carga de trabajo.  
  
#### <a name="to-enable-feedback"></a>Para habilitar los comentarios  
  
1.  Con una cuenta de administrador de dominio de aplicación, conéctese al nodo de Control (<strong>*appliance_domain*-CTL01</strong>) y abra un símbolo del sistema con sus credenciales de administrador de Windows.  
  
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
  
    1.  La primera vez que habilite la telemetría, use el siguiente comando para asegurarse de que todos los reenviadores DNS están configurados correctamente. En este ejemplo, reemplace la dirección IP de DNS reenvían `xx.xx.xx.xx` con la dirección IP del reenviador DNS en su entorno.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring -SetupDnsForwarder -DnsForwarderIp xx.xx.xx.xx  
        ```  
  
    2.  Cuando ya están configurados los reenviadores DNS, como volver a habilitar previamente deshabilitado telemetría, use el comando siguiente para habilitar la telemetría sin configurar el reenvío de DNS.  
  
        ```  
        PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Enable-RemoteMonitoring  
        ```  
  
5.  Se le indicará que lea y acepte que APS recopilará información sobre el dispositivo. Habrá un vínculo a la declaración de privacidad de puntos de acceso que puede copiar y pegar en cualquier explorador de internet para su revisión.  
  
6.  Escriba **Y** para aceptar y participar en los comentarios o escriba **N** no Aceptar.  
  
7.  Si escribió **Y** habrá una serie de comandos que se ejecutarán, lo que permitirá a los datos de telemetría (y opcionalmente el reenviador de DNS) características en el dispositivo. Si ve errores o información que lo conduce a creer que el comando no tuvo éxito póngase en contacto con CSS.  
  
Si escribió **N**, no hay ningún comando que se va a ejecutar y no se habilitará la característica y no hay nada más para hacer.  
  
No hay ningún riesgo en ejecución el `Enable-RemoteMonitoring` comando varias veces. Si ya se ha establecido el reenviador DNS obtendrá un mensaje de advertencia que indica que es el caso.  
  
## <a name="disable"></a>Deshabilitar la telemetría  
Deshabilitación de la telemetría se detendrá todas las operaciones que se comunican información sobre el estado del dispositivo a los puntos de acceso a la supervisión de servicio en la nube.  
  
> [!IMPORTANT]  
> Al realizar esta operación no se deshabilitará el reenviador DNS o la conexión a internet que puede estar en uso por otras características en el dispositivo.  
  
#### <a name="to-disable-telemetry"></a>Para deshabilitar la telemetría  
  
1.  Con una cuenta de administrador de dominio de aplicación, conéctese al nodo de Control (<strong>*appliance_domain*-CTL01</strong>) y abra una ventana de PowerShell con privilegios de administrador.  
  
2.  Navegue hasta el siguiente directorio: `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
3.  Importe el módulo `Configure-RemoteMonitoring.ps1`  
  
    > [!NOTE]  
    > Para importar debe usar dos puntos en el comando.  
  
    **Ejemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> . .\Configure-RemoteMonitoring.ps1  
    ```  
  
4.  Invocar el `Disable-RemoteMonitoring` comando sin parámetros. Este comando dejará de enviar comentarios. (Esto no afectará a la supervisión local.) Sin embargo, el comando no deshabilitar el reenviador de DNS o deshabilitar la conectividad a internet. Esto debe hacerse manualmente después de deshabilitar los comentarios correctamente.  
  
    **Ejemplo:**  
  
    ```  
    PS C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100> Disable-RemoteMonitoring  
    ```  
  
Si ve errores o información que lo conduce a creer que el comando no tuvo éxito póngase en contacto con CSS.  
  
No hay ningún riesgo en ejecución el `Disable-RemoteMonitoring` comando varias veces.  
  
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea:
- [Supervisión del dispositivo mediante el uso de la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
- [Supervisión del dispositivo mediante el uso de vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
- [Supervisión del dispositivo mediante el uso de System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
- [Usar un reenviador DNS para resolver nombres DNS que no sea de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
  
