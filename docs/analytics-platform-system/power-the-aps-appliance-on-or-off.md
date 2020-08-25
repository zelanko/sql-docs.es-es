---
title: Encendido o apagado del dispositivo
description: Encendido o apagado del dispositivo para el sistema de plataforma de análisis
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee70338b5a46ec60d808e489d982fd80692c5d1d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400620"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Encendido o apagado del dispositivo para el sistema de plataforma de análisis
En este tema se describe cómo encender o apagar la plataforma de análisis Systemappliance que ejecuta almacenamiento de datos paralelos. Use este tema cuando se mueva un dispositivo de sistema de plataforma de análisis o encienda un dispositivo después de un error grave en el suministro eléctrico.  
  
Encender y apagar el dispositivo no es lo mismo que iniciar y detener los servicios del dispositivo. Para obtener información sobre este tema, consulte el estado de los [servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md). Para obtener información sobre el encendido o apagado de un almacenamiento de datos paralelos SQL Server 2008, consulte el archivo de ayuda del almacenamiento de datos en paralelo de la SQL Server 2008. Para obtener información sobre el encendido o apagado de un almacenamiento de datos paralelos SQL Server 2012 AU1 o AU2, vea el archivo de ayuda de esas versiones.  
  
Cuando estas instrucciones especifican la conexión a un nodo de PDW de SQL Server, la conexión puede ser local mediante dispositivos conectados (KVM) o remotos mediante Escritorio remoto. Algunas acciones deben ser físicas (encendido de un interruptor de alimentación) y otras (como apagar) pueden ser físicas o mediante comandos de Windows.  
  
Las conexiones a los nodos PDW de SQL Server pueden realizarse mediante las direcciones IP asignadas a los nodos o desde el equipo **HST01** mediante las aplicaciones de **Administrador de clústeres de conmutación por error** (**CluAdmin. msc**) o **Administrador de Hyper-V** (**virtmgmt. msc**) y haciendo clic con el botón derecho en el nombre del nodo.  
  
## <a name="power-off-the-appliance"></a><a name="PowerOff"></a>Apagar el dispositivo  
  
### <a name="before-you-begin"></a>Antes de comenzar  
Antes de apagar el dispositivo, debe finalizar toda la actividad en el dispositivo. Para finalizar toda la actividad:  
  
-   Use la página **sesiones** de la consola de administración para identificar a los usuarios actuales. Póngase en contacto con ellos y pídale que cierre la sesión.  
  
-   Si es necesario, puede usar la instrucción **Kill** para forzar la finalización de una conexión de cliente. Tenga cuidado al eliminar conexiones. Cuando se interrumpe, algunos procesos transaccionales, como una actualización de larga ejecución, deben revertir la actividad antes de que SQL Server pueda completar la recuperación de la base de datos. La reversión de una actualización o eliminación completada parcialmente puede llevar mucho tiempo.  
  
### <a name="to-power-off-the-appliance"></a>Para apagar el dispositivo  
  
> [!WARNING]  
> Todos los pasos se deben realizar en el orden exacto indicado y cada paso debe completarse antes de que se realice el paso siguiente, a menos que se indique lo contrario. La realización de pasos desordenados o sin esperar a que se complete cada paso puede producir errores cuando el dispositivo se enciende en otro momento.  
  
1.  Conéctese al nodo de control de PDW (**_PDW_region_-CTL01** ) e inicie sesión con la cuenta de administrador de dominio de la plataforma de Analytics.  
  
2.  Ejecute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para abrir el **Configuration Manager**.  
  
3.  En el Configuration Manager, en el menú **topología de almacenamiento de datos paralelos** , haga clic en la pestaña Estado de los **servicios** y haga clic en **detener región** para detener los servicios de PDW.   
  
4.  Conéctese a ** _appliance_domain_-HST01** e inicie sesión con la cuenta de administrador de dominio de la aplicación.  
  
5.  Use el **Administrador de clústeres de conmutación por error** conectarse al clúster ** _appliance_domain_-WFOHST01** , si no está conectado automáticamente y, a continuación, en el panel de navegación, haga clic en **roles**. En el panel **roles** :  
  
    1.  Seleccione varias máquinas virtuales. Haga clic en ellos con el botón secundario y seleccione **apagar**.  
  
    2.  Espere a que finalice el cierre de todas las máquinas virtuales seleccionadas.  
  
6.  Cierre la aplicación **Administrador de clústeres de conmutación por error** .  
  
7. Cierre todos los servidores excepto ** _appliance_domain_-HST01**.  
  
8. Apague el servidor ** _appliance_domain_-HST01** .  
  
9. Apague las unidades de distribución de energía (PDU).  
  
## <a name="power-on-the-appliance"></a><a name="PowerOn"></a>Encender el dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Para encender el dispositivo  
  
> [!WARNING]  
> Todos los pasos se deben realizar en el orden exacto indicado y cada paso debe completarse antes de que se realice el paso siguiente, a menos que se indique lo contrario. La realización de pasos desordenados o sin esperar a que se complete cada paso puede dar lugar a errores de inicio.  
  
1.  Encienda las unidades de distribución de energía (PDU) y espere a que los conmutadores se inicien automáticamente.  
  
2.  Encienda el servidor de ** _appliance_domain_-HST01** .  
  
3.  Inicie sesión en ** _appliance_domain_-HST01** como administrador del dominio de la aplicación.  
  
4.  Inicie el programa **Administrador de Hyper-V** (**virtmgmt. msc**) y conéctese a ** _appliance_domain_-HST01** si no está conectado de forma predeterminada.  
  
    1.  Si no se puede conectar por nombre porque el ** _PDW_region_-AD01** no se está ejecutando, intente conectarse mediante la dirección IP.  
  
    2.  En el panel **virtual machines** , busque ** _PDW_region_-AD01** y confirme que se está ejecutando. Si no es así, inicie esta máquina virtual y espere a que se inicie completamente.  
  
5.  Encienda el resto de los servidores del dispositivo.  
  
6.  En **HST01** que ha iniciado sesión como administrador de dominio del dispositivo, desde el **Administrador de Hyper-V**:  
  
    1.  Conéctese a ** _appliance_domain_-HST02**.  
  
    2.  En el panel **virtual machines** , busque ** _PDW_region_-AD02** y confirme que se está ejecutando.  Si no es así, inicie esta máquina virtual y espere a que se inicie completamente.  
  
7.  Use el **Administrador de clústeres de conmutación por error** conectarse al clúster ** _appliance_domain_-WFOHST01** , si no está conectado automáticamente y, a continuación, en el panel de **navegación** , haga clic en **roles**. En el panel **roles** :  
  
    1.  Seleccione múltiples máquinas virtuales, haga clic en ellas con el botón secundario y, a continuación, haga clic en **iniciar**.  
  
    2.  Espere a que finalice el inicio de todas las máquinas virtuales seleccionadas antes de continuar con el siguiente paso.  
  
    3.  Si es necesario para las máquinas virtuales que conmutaron por error, ciérrela, muévalas y reinícielos en el host principal adecuado.  
  
8. Si lo desea, desconéctese de **HST01** .  
  
9. Conéctese a ** _PDW_region_-CTL01** con la cuenta de administrador de dominio de la aplicación.  
  
10. Ejecute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para iniciar el **Configuration Manager**.  
  
11. En el **Configuration Manager**, en el menú **topología de almacenamiento de datos paralelos** , haga clic en la pestaña Estado de los **servicios** y haga clic en la **región de inicio** para iniciar los servicios de PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Para comprobar el estado del dispositivo  
Una vez iniciado el dispositivo, abra la **consola de administración** y compruebe en la página de estado las alertas que podrían indicar condiciones de error. Para más información, consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Consulte también  
[Tareas de administración de dispositivos &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
