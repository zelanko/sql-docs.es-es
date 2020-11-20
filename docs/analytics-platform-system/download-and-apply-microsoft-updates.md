---
title: Descargar actualizaciones de Microsoft
description: En este tema se describe cómo descargar actualizaciones del catálogo de Microsoft Update a Windows Server Update Services (WSUS) y cómo aplicarlas a los servidores del dispositivo de análisis de plataforma. Microsoft Update instalará todas las actualizaciones aplicables para Windows y SQL Server. WSUS está instalado en la máquina virtual de VMM del dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e5f336c3c2c475523d2081bcf01189e67b77fe19
ms.sourcegitcommit: ce15cbbcb0d5f820f328262ff5451818e508b480
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2020
ms.locfileid: "94947920"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Descargar y aplicar actualizaciones de Microsoft para el sistema de plataforma de análisis
En este tema se describe cómo descargar actualizaciones del catálogo de Microsoft Update a Windows Server Update Services (WSUS) y cómo aplicarlas a los servidores del dispositivo de análisis de plataforma. Microsoft Update instalará todas las actualizaciones aplicables para Windows y SQL Server. WSUS está instalado en la máquina virtual de VMM del dispositivo.  
  
## <a name="before-you-begin"></a><a name="TOP"></a>Antes de empezar  
  
> [!WARNING]  
> No intente aplicar actualizaciones si el dispositivo o cualquier componente del dispositivo está inactivo o en un estado de conmutación por error. En ese caso, póngase en contacto con soporte técnico para obtener ayuda.  
>   
> No aplique actualizaciones de Microsoft mientras el dispositivo esté en uso. La aplicación de actualizaciones puede hacer que los nodos del dispositivo se reinicien. Las actualizaciones deben aplicarse durante una ventana de mantenimiento cuando no se usa el dispositivo.  
  
### <a name="prerequisites"></a>Requisitos previos  
Antes de realizar estos pasos, debe hacer lo siguiente:  
  
-   Configure WSUS en el dispositivo siguiendo las instrucciones de [configuración de Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
-   Conocimiento de la información de inicio de sesión de una cuenta de administrador de dominio de tejido.  
  
-   Tener un inicio de sesión con permisos para tener acceso a la consola de administración del sistema de la plataforma de análisis y ver la información de estado del dispositivo.  
  
-   En la mayoría de los casos, WSUS necesita acceder a los servidores fuera del dispositivo. Para admitir este escenario de uso, el DNS del sistema de plataforma de análisis puede configurarse para admitir un reenviador de nombres externo que permita que los hosts de sistema de la plataforma de análisis y el Virtual Machines (VM) usen servidores DNS externos para resolver nombres fuera del dispositivo. Para obtener más información, consulte [uso de un reenviador DNS para resolver nombres DNS que no son de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-download-and-apply-microsoft-updates"></a><a name="bkmk_ImportUpdates"></a>Para descargar y aplicar actualizaciones de Microsoft  
  
#### <a name="verify-the-appliance-state-indicators"></a>Comprobar los indicadores de estado del dispositivo  
  
1.  Abra la consola de administración de y vaya a la página estado del dispositivo. Para más información, consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Compruebe los indicadores de estado de todos los nodos en el estado del dispositivo.  
  
    -   Es seguro continuar con los indicadores verde o NA.  
  
    -   Evaluar errores de advertencia no críticos (amarillos). En algunos casos, los mensajes de advertencia no bloquearán las actualizaciones. Si hay un error de volumen de disco no crítico que no está en el C:\ , puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
    -   La mayoría de los indicadores rojos se deben resolver antes de continuar. Si hay errores de disco, use la página de alertas de la consola de administración para comprobar que no haya más de un error de disco dentro de cada matriz de servidores o SAN. Si no hay más de un error de disco dentro de cada matriz de servidores o SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con el soporte técnico de Microsoft para corregir los errores de disco lo antes posible.  
  
#### <a name="synchronize-the-wsus-server"></a>Sincronizar el servidor WSUS  
  
1.  Inicie sesión en la máquina virtual de VMM como administrador de dominio.  
  
2.  En el **Panel de administrador del servidor**, en el menú **herramientas** , haga clic en **Windows Server Update Services** (**WSUS. msc**).  
  
3.  En la consola de administración de WSUS, haga clic en **sincronizaciones**.  
  
4.  Si no se está ejecutando la sincronización, haga clic en **sincronizar ahora** en el panel derecho. En el panel inferior, habrá un estado de sincronización. Espere hasta que se complete la sincronización.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Aprobar actualizaciones de Microsoft en WSUS  
  
1. Rechazar los paquetes acumulativos de actualizaciones que no sean de **System Center**.

2. En el panel izquierdo de la consola de WSUS, haga clic en **todas las actualizaciones**.  
  
3.  En el panel **todas las actualizaciones** , haga clic en el menú desplegable **aprobación** , establezca **aprobación** en **cualquiera excepto rechazado**. Haga clic en el menú desplegable **Estado** y establezca **Estado** en **cualquiera**. Haga clic en **Actualizar**.  
  
    Haga clic con el botón derecho en la columna **título** y seleccione **Estado del archivo** para comprobar el estado del archivo una vez completada la descarga.  
  
    También puede seleccionar **actualizaciones críticas** o **actualizaciones de seguridad** en el panel izquierdo y ver las actualizaciones disponibles para estas categorías.  
  
    ![Seleccione todas las actualizaciones y cambie el estado a Cualquiera.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
4.  Seleccione todas las actualizaciones y, a continuación, haga clic en el vínculo **aprobar** en el panel derecho.  
  
    También puede hacer clic con el botón secundario en las actualizaciones seleccionadas y, a continuación, hacer clic en **aprobar**. Es posible que se le pida que acepte los términos de licencia del software de Microsoft. Si es así, **haga clic en Acepto en** la ventana para continuar.  
  
    ![Seleccione todas las actualizaciones aplicables y haga clic en Aprobar.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
5.  Seleccione el grupo de servidores de dispositivo que creó en [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
6.  Haga clic en **Aprobada para su instalación** y, a continuación, en **Aceptar**.  
  
    ![Aprobar actualizaciones para el grupo de equipos.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
7.  En el cuadro de diálogo progreso de la **aprobación** , cuando se complete el proceso de aprobación, haga clic en **cerrar**.  
  
    ![Cerrar ventana una vez aprobadas las actualizaciones](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Comprobar que las actualizaciones están en WSUS  
  
-  Compruebe el estado del archivo de todas las actualizaciones. Cada archivo debe tener un icono de flecha verde a la izquierda del título. Esto indica que el archivo está listo para la instalación.  
  
    ![El estado de archivo es correcto](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Antes de instalar las actualizaciones, asegúrese de que todas se han descargado y están disponibles en la consola de WSUS.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Para comprobar que se han descargado todas las actualizaciones  
  
-  Compruebe el **Estado de descarga** de las actualizaciones en la consola de WSUS, tal como se muestra en la siguiente captura de pantalla. Compruebe que **las actualizaciones que necesitan archivos** sean 0 para confirmar que se han descargado todas las actualizaciones. Si este número es mayor que cero, puede que necesite volver atrás y aprobar actualizaciones adicionales.  
  
    ![Comprobar que se han descargado todas las actualizaciones.](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Aplicar actualizaciones de Microsoft  
  
1.  Antes de empezar, abra el [monitor del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md), haga clic en la pestaña **Estado del dispositivo** y compruebe que las columnas del **clúster** y de la **red** muestran el verde (o el na) de todos los nodos. Si hay alguna alerta en cualquiera de estas columnas, es posible que el dispositivo no pueda instalar las actualizaciones correctamente. Solucione todas las alertas existentes en las columnas de **clúster** y de **red** antes de continuar.  
  
2.  Inicie sesión en el _<domain_name nodo>_ **-HST01** como administrador del dominio del tejido.  
  
3.  Para aplicar todas las actualizaciones aprobadas para WSUS, ejecute el programa de actualización. Consulte [ejecutar el programa de actualización](#RunUpdateWizard) siguiente para obtener instrucciones.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Comprobar las actualizaciones en todos los nodos  
  
1.  En el nodo VMM, inicie la consola de administración de WSUS. Esta aplicación se puede encontrar en **Inicio**, **herramientas administrativas** **Windows Server Update Services**.  
  
2.  Expanda **equipos**.  
  
3.  Expanda **todos los equipos**.  
  
4.  Seleccione el grupo de servidores de dispositivo que creó en [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  En el menú desplegable **Estado** , seleccione **cualquiera** y haga clic en **Actualizar**.  
  
6.  Expanda **servicios de actualización**, *<appliance name>* -VMM, **actualizaciones**, **todas las actualizaciones**, donde *<appliance name>* es el nombre del dispositivo.  
  
7.  En la ventana **todas las actualizaciones** , establezca **aprobación** en **cualquiera, excepto rechazado**.  
  
8.  En la ventana **todas las actualizaciones** , establezca el **Estado** en **error o en necesario**.  
  
9. Haga clic en **Actualizar**.  
  
10. Si **las actualizaciones necesarias** son mayores que cero, póngase en contacto con el soporte técnico para obtener ayuda.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Asegúrese de que no hay ninguna alerta crítica en la consola de administración de PDW de SQL Server  
  
1.  Abra la consola de administración de, haga clic en la pestaña Estado del dispositivo. Consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Compruebe que las columnas de **clúster** y de **red** muestran el verde (o el na) de todos los nodos. Si hay alguna alerta en cualquiera de estas columnas, es posible que el dispositivo no pueda instalar las actualizaciones correctamente. Póngase en contacto con soporte técnico si hay alertas críticas.  
  
## <a name="run-the-update-program"></a><a name="RunUpdateWizard"></a>Ejecutar el programa de actualización  
Siga estas instrucciones para ejecutar el programa de actualización del sistema de análisis de plataforma.  
  
> [!NOTE]  
> El sistema WSUS está diseñado para ejecutarse de forma asincrónica, por lo que puede tardar algún tiempo en aplicar todas las actualizaciones. Al iniciar una actualización, se programa una actualización, pero no se garantiza la actividad de actualización inmediata.  
  
1.  Asegúrese de que ha iniciado sesión en el nodo HST01 como el administrador del dominio de tejido.  
  
2.  Abra una ventana del símbolo del sistema y escriba los siguientes comandos. Reemplazar *<parameter>* por la información designada.  
  
**Para ejecutar el Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Para notificar el estado de la Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Consulte también  
[Desinstale Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicación de revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Desinstalación de las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Servicio de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
