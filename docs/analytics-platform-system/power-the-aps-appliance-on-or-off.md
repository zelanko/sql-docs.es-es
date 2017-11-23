---
title: "Alimentación del dispositivo de APS o desactivar (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2258f8e3-e7a1-4455-8a5e-10d4d15775d6
caps.latest.revision: "45"
ms.openlocfilehash: 3264c3f97f765e9a62a38987638bdf2a8b13e82b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="power-the-aps-appliance-on-or-off"></a>Encender el dispositivo de APS o apagar
En este tema se describe cómo encender o apagar el Systemappliance de plataforma de análisis que se ejecuta el almacenamiento de datos paralelos y, opcionalmente, ejecuta una región de HDInsight. Utilice este tema cuando se mueve un dispositivo de sistema de la plataforma de análisis, o a la potencia en un dispositivo después de un error de alimentación grave.  
  
Activando el dispositivo y desactivar no es el mismo que iniciar y detener los servicios del dispositivo. Para obtener información acerca de ese tema, consulte [estado de los servicios PDW &#40; Sistema de la plataforma de análisis &#41; ](pdw-services-status.md). Para obtener información acerca de cómo activar y activar o desactivar un almacenamiento de datos paralelo de SQL Server 2008, consulte el archivo de Ayuda de almacenamiento de datos paralelo de SQL Server 2008. Para obtener información acerca de cómo activar y activar o desactivar un SQL Server 2012 AU1 o almacenamiento de datos paralelos de AU2, consulte el archivo de ayuda para esas versiones.  
  
Cuando estas instrucciones especifican la conexión a un nodo de SQL Server PDW, la conexión puede ser local con los dispositivos conectados (KVM) o remoto mediante Escritorio remoto. Algunas acciones deben ser física (al activar un interruptor de alimentación) y otras (por ejemplo, apagado) puede ser físico o mediante Windows comandos.  
  
Conexiones a los nodos de SQL Server PDW pueden realizarse con las direcciones IP asignadas a los nodos, o desde el **HST01** equipo utilizando la **Administrador de clústeres de conmutación por error** (**cluadmin.msc**) o **Administrador de Hyper-V** (**virtmgmt.msc**) con el botón secundario el nombre del nodo y aplicaciones.  
  
## <a name="PowerOff"></a>Apagar el dispositivo  
  
### <a name="before-you-begin"></a>Antes de empezar  
Antes de apagar el dispositivo, debe finalizar todas las actividades en el dispositivo. Para finalizar todas las actividades:  
  
-   Use la **sesiones** página de la consola de administración para identificar los usuarios actuales. Póngase en contacto con ellos y pídale que cierre la sesión.  
  
-   Si es necesario puede utilizar el **KILL** instrucción para forzar la finalización de una conexión de cliente. Tenga cuidado al eliminar conexiones. Cuando se interrumpe, algunos procesos transaccionales, como una actualización de ejecución prolongada, debe actividad de reversión antes de SQL Server puede completar la recuperación de la base de datos. Revertir una actualización parcialmente completada o eliminación, puede llevar mucho tiempo.  
  
### <a name="to-power-off-the-appliance"></a>Para apagar el dispositivo  
  
> [!WARNING]  
> Todos los pasos deben realizarse en el orden exacto mostrado y debe completar cada paso antes de realiza el paso siguiente, a menos que se indique lo contrario. Realizar pasos fuera de servicio o sin tener que esperar para que se complete cada paso puede producir errores cuando el dispositivo se enciende en un momento posterior.  
  
1.  Conéctese al nodo de Control de PDW (***PDW_region*-CTL01** ) e inicie sesión con la cuenta de administrador de dominio de aplicación de sistema de la plataforma de análisis.  
  
2.  Ejecutar `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para abrir el **Configuration Manager**.  
  
3.  En el Administrador de configuración, en la **topología de almacenamiento de datos paralelos** menú, haga clic en el **estado de los servicios** ficha y haga clic en **detener región** para detener los servicios PDW.  
  
4.  Si hay una región de HDInsight en el **HDInsight topología** menú, haga clic en el **estado de los servicios** ficha y haga clic en **detener región** para detener los servicios de HDInsight.  
  
5.  Conectarse a  ***appliance_domain*-HST01** e inicie sesión con la cuenta de administrador de dominio de aplicación.  
  
6.  Mediante el **Administrador de clústeres de conmutación por error** conectarse a la  ***appliance_domain*-WFOHST01** de clúster, si se conecta automáticamente y, a continuación, en el panel de navegación, haga clic en **Roles**. En el **Roles** panel:  
  
    1.  Selección múltiple de todas las máquinas virtuales. El botón secundario y seleccione **apagar**.  
  
    2.  Espere a que todas las máquinas virtuales seleccionadas al finalizar va a cerrar.  
  
7.  Si hay una región de HDInsight:  
  
    1.  Conéctese al clúster de HDInsight. Para ello, haga doble clic en **Administrador de clústeres de conmutación por error**, seleccione **conectar al clúster**y especifique  ***appliance_domain*-WFOHST02** el nombre del clúster.  
  
    2.  En el clúster de HDInsight, haga clic en **Roles**. En el **Roles** panel:  
  
        1.  Selección múltiple de todas las máquinas virtuales, el botón secundario y seleccione **apagar**.  
  
        2.  Espere a que apagar las máquinas virtuales.  
  
8.  Cerrar la **Administrador de clústeres de conmutación por error** aplicación.  
  
9. Cierre todos los servidores excepto  ***appliance_domain*-HST01**.  
  
10. Apagar el  ***appliance_domain*-HST01** server.  
  
11. Apague las unidades de distribución de energía (PDU).  
  
## <a name="PowerOn"></a>Encienda el dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Para encender el dispositivo  
  
> [!WARNING]  
> Todos los pasos deben realizarse en el orden exacto mostrado y debe completar cada paso antes de realiza el paso siguiente, a menos que se indique lo contrario. Realizar pasos fuera de servicio o sin tener que esperar para que se complete cada paso puede dar lugar a errores de inicio.  
  
1.  Encienda el unidades de distribución de energía (PDU) y espere a que los conmutadores para iniciarse automáticamente.  
  
2.  Encender el  ***appliance_domain*-HST01** server.  
  
3.  Inicie sesión en  ***appliance_domain*-HST01** como administrador del dominio de aplicación.  
  
4.  Iniciar el **Administrador de Hyper-V** programa (**virtmgmt.msc**) y conéctese a  ***appliance_domain*-HST01** si no está conectado de forma predeterminada.  
  
    1.  Si no se puede conectar por nombre porque el  ***PDW_region*-AD01** es no ejecutando, intente conectarse mediante la dirección IP.  
  
    2.  En el **máquinas virtuales** panel, busque  ***PDW_region*-AD01** y confirme que se está ejecutando. Si no es así, inicie esta máquina virtual y espere a que se haya iniciado totalmente.  
  
5.  Encienda el resto de los servidores en el dispositivo.  
  
6.  En **HST01** han iniciado sesión como administrador del dominio de aplicación, **Administrador de Hyper-V**:  
  
    1.  Conectarse a  ***appliance_domain*-HST02**.  
  
    2.  En el **máquinas virtuales** panel, busque  ***PDW_region*-AD02** y confirme que se está ejecutando.  Si no es así, inicie esta máquina virtual y espere a que se haya iniciado totalmente.  
  
7.  Mediante el **Administrador de clústeres de conmutación por error** conectarse a la  ***appliance_domain*-WFOHST01** en clúster, si no automáticamente conectado y, a continuación, en la  **Navegación** panel, haga clic en **Roles**. En el **Roles** panel:  
  
    1.  Selección múltiple de todas las máquinas virtuales, haga clic en ellos y, a continuación, haga clic en **iniciar**.  
  
    2.  Espere a que todas las máquinas virtuales seleccionadas terminen de iniciarse antes de continuar con el paso siguiente.  
  
    3.  Si es necesario para las máquinas virtuales que conmutar por error, apagarlos, moverlos y reiniciarlas una vez en el host primario correcto.  
  
8.  Si el dispositivo tiene una región de HDInsight, conéctese al clúster de HDInsight. (Para ello, haga doble clic en **Administrador de clústeres de conmutación por error**, seleccione **conectar al clúster**y especifique  ***appliance_domain*-WFOHST01** para el nombre de clúster).  
  
    1.  En el clúster de HDInsight, haga clic en **Roles**. En el **Roles** panel.  
  
        1.  Selección múltiple de todas las máquinas virtuales, el botón secundario y seleccione **iniciar**,  
  
        2.  Espere a que todas las máquinas virtuales seleccionadas terminen de iniciarse antes de continuar con el paso siguiente.  
  
        3.  Si es necesario para las máquinas virtuales que conmutar por error, apagarlos, moverlos y reiniciarlas una vez en el host primario correcto.  
  
9. Desconectarse de **HST01** si lo desea.  
  
10. Conectarse a  ***PDW_region*-CTL01** con la cuenta de administrador de dominio de aplicación.  
  
11. Ejecutar `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para iniciar el **Configuration Manager**.  
  
12. En el **Configuration Manager**, en la **topología de almacenamiento de datos paralelos** menú, haga clic en el **estado de los servicios** ficha y haga clic en **iniciar región**para iniciar los servicios PDW.  
  
13. Si el dispositivo tiene una región de HDInsight, en el menú de la topología de HDInsight, haga clic en el **estado de los servicios** ficha y haga clic en **iniciar región** para iniciar los servicios de HDInsight.  
  
### <a name="to-verify-the-appliance-health"></a>Para comprobar el estado de dispositivo  
Una vez iniciada la aplicación, abra el **consola de administración de** y compruebe la página de mantenimiento para las alertas que podrían indicar condiciones de error. Para obtener más información, vea [supervisar el dispositivo mediante la consola de administración &#40; Sistema de la plataforma de análisis &#41; ](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Vea también  
[Tareas de administración de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-management-tasks.md)  
  
