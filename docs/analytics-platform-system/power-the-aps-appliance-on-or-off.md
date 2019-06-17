---
title: Conecte el dispositivo o desactivar - Analytics Platform System | Microsoft Docs
description: Alimentación del dispositivo o desactivar para Analytics Platform System
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 994b0f94448b7fb7901734b2ae737e26be23900f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62678633"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Alimentación del dispositivo o desactivar para Analytics Platform System
Este tema describe cómo a encendido o apagado su Systemappliance de plataforma de análisis ejecuta con almacenamiento de datos paralelos. Use este tema cuando se mueve una aplicación Analytics Platform System, o a la potencia en un dispositivo tras un error grave de energía.  
  
Activar el dispositivo y desactivar no es el mismo que iniciar y detener los servicios del dispositivo. Para obtener información sobre ese tema, consulte [estado de servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md). Para obtener información sobre cómo activar o desactivar un almacenamiento de datos paralelos de SQL Server 2008, vea el archivo de Ayuda de almacenamiento de datos paralelos de SQL Server 2008. Para obtener información sobre cómo activar o desactivar un SQL Server 2012 AU1 o AU2 Parallel Data Warehouse, consulte el archivo de ayuda para esas versiones.  
  
Cuando estas instrucciones especifican conectar a un nodo PDW de SQL Server, la conexión puede ser local con los dispositivos conectados (KVM) o remoto mediante Escritorio remoto. Algunas acciones deben ser física (al activar un interruptor de alimentación) y algunos (por ejemplo, apagado) puede ser físico o mediante el uso de Windows, los comandos.  
  
Las conexiones a los nodos de PDW de SQL Server pueden realizarse con las direcciones IP asignadas a los nodos, o desde el **HST01** equipo mediante el uso del **Administrador de clústeres de conmutación por error** (**cluadmin.msc**) o **Administrador de Hyper-V** (**virtmgmt.msc**) las aplicaciones y haciendo clic en el nombre del nodo.  
  
## <a name="PowerOff"></a>Apagar el dispositivo  
  
### <a name="before-you-begin"></a>Antes de comenzar  
Antes de apagar el dispositivo, debe terminar todas las actividades en el dispositivo. Para finalizar todas las actividades:  
  
-   Use la **sesiones** página de la consola de administración para identificar los usuarios actuales. Póngase en contacto con ellos y pídale que cierre la sesión.  
  
-   Si es necesario puede utilizar el **KILL** instrucción para forzar la terminación de una conexión de cliente. Tenga cuidado al eliminar conexiones. Cuando se interrumpe, algunos procesos transaccionales, como una actualización de ejecución prolongada, debe actividad reversión antes de que SQL Server puede completar la recuperación de la base de datos. Revertir una actualización parcialmente completada o la eliminación, puede tardar mucho tiempo.  
  
### <a name="to-power-off-the-appliance"></a>Para apagar el dispositivo  
  
> [!WARNING]  
> Todos los pasos deben realizarse en el orden exacto mostrado y debe completar cada paso antes de realiza el paso siguiente, a menos que se indique lo contrario. Estos pasos desordenados o sin tener que esperar para que completar cada paso pueden provocar errores cuando se encienda el dispositivo en un momento posterior.  
  
1.  Conéctese al nodo de Control de PDW ( **_PDW_region_-CTL01** ) e inicie sesión con la cuenta de administrador de dominio de Analytics Platform System appliance.  
  
2.  Ejecute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para abrir el **Configuration Manager**.  
  
3.  En Configuration Manager, en el **topología de almacenamiento de datos paralela** menú, haga clic en el **estado Services** ficha y haga clic en **detener región** para detener los servicios PDW.   
  
4.  Conectarse a  **_appliance_domain_-HST01** e inicie sesión con la cuenta de administrador de dominio de aplicación.  
  
5.  Mediante el **Administrador de clústeres de conmutación por error** conectarse a la  **_appliance_domain_-WFOHST01** del clúster, si se conecta automáticamente y, a continuación, en el panel de navegación, haga clic en **Roles**. En el **Roles** panel:  
  
    1.  Selección múltiple de todas las máquinas virtuales. El botón derecho y seleccione **apagar**.  
  
    2.  Espere a que todas las máquinas virtuales seleccionadas finalizar la va a cerrar.  
  
6.  Cerrar la **Administrador de clústeres de conmutación por error** aplicación.  
  
7. Apagar todos los servidores excepto  **_appliance_domain_-HST01**.  
  
8. Apagar el  **_appliance_domain_-HST01** server.  
  
9. Apague las unidades de distribución de energía (PDU).  
  
## <a name="PowerOn"></a>Encienda el dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Para encender el dispositivo  
  
> [!WARNING]  
> Todos los pasos deben realizarse en el orden exacto mostrado y debe completar cada paso antes de realiza el paso siguiente, a menos que se indique lo contrario. Estos pasos desordenados o sin tener que esperar para que completar cada paso pueden dar lugar a errores de inicio.  
  
1.  Encienda la unidades de distribución de energía (PDU) y espere a que los conmutadores para iniciarse automáticamente.  
  
2.  Encender el  **_appliance_domain_-HST01** server.  
  
3.  Inicie sesión en  **_appliance_domain_-HST01** como administrador del dominio de aplicación.  
  
4.  Iniciar el **Administrador de Hyper-V** programa (**virtmgmt.msc**) y conéctese a  **_appliance_domain_-HST01** si no está conectado de forma predeterminada.  
  
    1.  Si no se puede conectar por nombre porque el  **_PDW_region_-AD01** es no se está ejecutando, intente conectarse mediante el uso de la dirección IP.  
  
    2.  En el **máquinas virtuales** panel, busque  **_PDW_region_-AD01** y confirme que se está ejecutando. Si no es así, inicie esta máquina virtual y espere a que se haya iniciado totalmente.  
  
5.  Encienda el resto de los servidores en el dispositivo.  
  
6.  Mientras que en **HST01** han iniciado sesión como administrador del dominio de aplicación, **Administrador de Hyper-V**:  
  
    1.  Conectarse a  **_appliance_domain_-HST02**.  
  
    2.  En el **máquinas virtuales** panel, busque  **_PDW_region_-AD02** y confirme que se está ejecutando.  Si no es así, inicie esta máquina virtual y espere a que se haya iniciado totalmente.  
  
7.  Mediante el **Administrador de clústeres de conmutación por error** conectarse a la  **_appliance_domain_-WFOHST01** en clúster, si se conecta automáticamente y, a continuación, en el  **Navegación** panel, haga clic en **Roles**. En el **Roles** panel:  
  
    1.  Selección múltiple de todas las máquinas virtuales, haga clic en ellos y, a continuación, haga clic en **iniciar**.  
  
    2.  Espere a que todas las máquinas virtuales seleccionadas terminen de iniciarse antes de continuar con el paso siguiente.  
  
    3.  Si es necesario para las máquinas virtuales que conmutan por error, apagarlas, moverlos y reiniciarlas en el host primario correcto.  
  
8. Desconectarse de **HST01** si lo desea.  
  
9. Conectarse a  **_PDW_region_-CTL01** con la cuenta de administrador de dominio de aplicación.  
  
10. Ejecute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para iniciar el **Configuration Manager**.  
  
11. En el **Configuration Manager**, en el **topología de almacenamiento de datos paralela** menú, haga clic en el **estado Services** ficha y haga clic en **iniciar región**para iniciar los servicios PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Para comprobar el estado del dispositivo  
Una vez se ha iniciado el dispositivo, abra el **Admin Console** y compruebe la página de mantenimiento para las alertas que podrían indicar las condiciones de error. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Vea también  
[Tareas de administración de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
