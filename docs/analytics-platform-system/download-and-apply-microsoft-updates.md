---
title: Descargar actualizaciones de Microsoft - Analytics Platform System | Microsoft Docs
description: En este tema se describe cómo descargar actualizaciones desde el catálogo de Microsoft Update para Windows Server Update Services (WSUS) y esas actualizaciones se aplican a los servidores de Analytics Platform System appliance. Microsoft Update se instalará todas las actualizaciones aplicables para Windows y SQL Server. WSUS está instalado en la máquina virtual VMM del dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d71a6ddc965b422f0f96f40788352213501b4db2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042350"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Descargue y aplique las actualizaciones de Microsoft para Analytics Platform System
En este tema se describe cómo descargar actualizaciones desde el catálogo de Microsoft Update para Windows Server Update Services (WSUS) y esas actualizaciones se aplican a los servidores de Analytics Platform System appliance. Microsoft Update se instalará todas las actualizaciones aplicables para Windows y SQL Server. WSUS está instalado en la máquina virtual VMM del dispositivo.  
  
## <a name="TOP"></a>Antes de empezar  
  
> [!WARNING]  
> No intente aplicar actualizaciones si su dispositivo o cualquier componente de dispositivo está desconectado o está en un error sobre el estado. En ese caso, póngase en contacto con soporte técnico para obtener ayuda.  
>   
> No se aplican Microsoft Updates mientras el dispositivo está en uso. Aplicar las actualizaciones para hacer que los nodos del dispositivo se reinicie. Las actualizaciones se deben aplicar durante una ventana de mantenimiento cuando no se usa el dispositivo.  
  
### <a name="prerequisites"></a>Requisitos previos  
Antes de realizar estos pasos, necesitará:  
  
-   Configurar WSUS en el dispositivo siguiendo las instrucciones de [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
-   Conocimiento de un información de inicio de sesión de cuenta de administrador de dominio del tejido.  
  
-   Tener un inicio de sesión con permisos para tener acceso a la consola de administración del sistema de plataforma de análisis y ver información de estado del dispositivo.  
  
-   En la mayoría de los casos, WSUS necesita acceso a los servidores están fuera de la aplicación. Para admitir este escenario de uso, el sistema de plataforma de análisis de DNS puede configurarse para admitir un reenviador de nombre externo que permitirá a los hosts de Analytics Platform System y la máquinas virtuales (VM) usar servidores DNS externos para resolver nombres fuera de la dispositivo. Para obtener más información, consulte [usar un reenviador DNS para resolver los nombres DNS que no son de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="bkmk_ImportUpdates"></a>Para descargar y aplicar las actualizaciones de Microsoft  
  
#### <a name="verify-the-appliance-state-indicators"></a>Compruebe los indicadores de estado de dispositivo  
  
1.  Abra la consola de administración y navegue a la página de estado del dispositivo. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Compruebe los indicadores de estado para todos los nodos en el estado del dispositivo.  
  
    -   Es seguro continuar con el color verde o indicadores NA.  
  
    -   Evaluar errores no críticos de advertencia (amarillo). En algunos casos los mensajes de advertencia no bloqueará las actualizaciones. Si se produce un error de volumen de disco no críticos que no está en la unidad C:\, puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
    -   La mayoría de los indicadores rojo se deben resolver antes de continuar. Si hay errores de disco, use la página de alertas de la consola de administrador para comprobar que no más de un error de disco en cada servidor o una matriz de SAN. Si se produce un error de no más de un disco en cada servidor o una matriz de SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con soporte técnico de Microsoft para corregir los errores de disco tan pronto como sea posible.  
  
#### <a name="synchronize-the-wsus-server"></a>Sincronizar el servidor WSUS  
  
1.  Inicie sesión en la máquina virtual VMM como un administrador de dominio.  
  
2.  En el **panel Administrador del servidor**, en el **herramientas** menú, haga clic en **Windows Server Update Services** (**wsus.msc**).  
  
3.  En la consola de administración de WSUS, haga clic en **sincronizaciones**.  
  
4.  Si no se está ejecutando la sincronización, haga clic en **sincronizar ahora** en el panel derecho. En el panel inferior, habrá un estado de sincronización. Espere hasta que se ha completado la sincronización.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Aprobar las actualizaciones de Microsoft en WSUS  
  
1.  En el panel izquierdo de la consola WSUS, haga clic en **todas las actualizaciones**.  
  
2.  En el **todas las actualizaciones** panel, haga clic en el **aprobación** menú desplegable, establezca **aprobación** a **cualquier excepción rechazada**. Haga clic en el **estado** menú desplegable, establezca **estado** a **cualquier**. Haga clic en **Actualizar**.  
  
    Haga clic en el **título** columna y seleccione **estado del archivo** para comprobar el estado del archivo una vez finalizada la descarga.  
  
    También puede seleccionar **actualizaciones críticas** o **las actualizaciones de seguridad** en el izquierdo panel y ver actualizaciones disponibles para estas categorías.  
  
    ![Seleccione todas las actualizaciones y cambie el estado a cualquiera. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  Seleccione todas las actualizaciones y, a continuación, haga clic en el **aprobar** vínculo en el panel derecho.  
  
    Puede también haga clic en las actualizaciones seleccionadas y, a continuación, haga clic en **aprobar**. Se pedirá que acepte los "términos de licencia de Software de Microsoft". Si es así, haga clic en **acepto** en la ventana para continuar.  
  
    ![Seleccione todas las actualizaciones aplicables y haga clic en Aprobar. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  Seleccione el grupo de servidores de dispositivo que creó en [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  Haga clic en **aprobada para su instalación**y, a continuación, haga clic en **Aceptar**.  
  
    ![Aprobar actualizaciones para el grupo de equipos. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  En el **progreso de la aprobación** cuadro de diálogo, cuando el proceso de aprobación se completa, haga clic en **cerrar**.  
  
    ![Cierre la ventana cuando se aprueban las actualizaciones. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Comprobar que las actualizaciones en WSUS  
  
-  Compruebe el estado de todas las actualizaciones del archivo. Cada archivo debe tener un icono de flecha verde hacia la izquierda del título. Esto indica que el archivo está listo para la instalación.  
  
    ![File status is successful](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Antes de instalar las actualizaciones, asegúrese de que son todas descargado y está disponible en la consola de WSUS.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Para comprobar que todas las actualizaciones se descargan  
  
-  Compruebe el **descargar estado** de actualizaciones en la consola WSUS, como se muestra en la captura de pantalla siguiente. Compruebe que **las actualizaciones que necesita archivos** es 0 para confirmar que todas las actualizaciones se descargan. Si este número es mayor que cero, es posible que deba volver atrás y aprobar actualizaciones adicionales.  
  
    ![Compruebe que todas las actualizaciones se descargan. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Aplicar actualizaciones de Microsoft  
  
1.  Antes de empezar, abra el [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md), haga clic en el **estado de dispositivo** pestaña y compruebe que la  **Clúster** y **red** show verde columnas (o ND) para todos los nodos. Si existe alguna alerta en cualquiera de estas columnas, el dispositivo no pueda instalar correctamente las actualizaciones. Resolver todas las alertas existentes en el **clúster** y **red** columnas antes de continuar.  
  
2.  Inicie sesión en el _< nombreDeDominio >_ **-HST01** nodo como el Administrador de dominio de Fabric.  
  
3.  Para aplicar todas las actualizaciones aprobadas para WSUS, ejecute el programa de actualización. Consulte [ejecutar el programa de actualización](#RunUpdateWizard) a continuación para obtener instrucciones.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Comprobar las actualizaciones en todos los nodos  
  
1.  En el nodo de VMM, inicie la consola de administración de WSUS. Esta aplicación se puede encontrar en **iniciar**, **herramientas administrativas**, **Windows Server Update Services**.  
  
2.  Expanda **equipos**.  
  
3.  Expanda **todos los equipos**.  
  
4.  Seleccione el grupo de servidores de dispositivo que creó en [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  En el **estado** menú desplegable, seleccione **cualquier** y haga clic en **actualizar**.  
  
6.  Expanda **actualizar servicios**, *<appliance name>* - VMM, **actualizaciones**, **todas las actualizaciones**, donde *<appliance name>* es el nombre de dispositivo.  
  
7.  En el **todas las actualizaciones** ventana conjunto **aprobación** a **cualquier excepción rechazada**.  
  
8.  En el **todas las actualizaciones** ventana, establezca **estado** a **error o necesita**.  
  
9. Haga clic en **Actualizar**.  
  
10. Si **las actualizaciones necesarias** es mayor que cero, póngase en contacto con soporte para obtener ayuda.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Asegúrese de que no hay ninguna alerta crítica en la consola de administración de SQL Server PDW  
  
1.  Abra la consola de administración, haga clic en la ficha de estado del dispositivo. Consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Compruebe que la **clúster** y **red** show verde columnas (o ND) para todos los nodos. Si existe alguna alerta en cualquiera de estas columnas, el dispositivo no pueda instalar correctamente las actualizaciones. Si hay alguna alerta crítica, póngase en contacto con soporte técnico.  
  
## <a name="RunUpdateWizard"></a>Ejecute el programa de actualización  
Siga estas instrucciones para ejecutar el programa de actualización del sistema de plataforma de análisis.  
  
> [!NOTE]  
> El sistema WSUS está diseñado para ejecución asincrónica puede tardar algún tiempo en todas las actualizaciones se aplican totalmente. Iniciar una actualización programa una actualización pero no garantiza la actividad de actualización inmediata.  
  
1.  Asegúrese de que se registran en el nodo HST01 como administrador de dominio de Fabric.  
  
2.  Abra una ventana del símbolo del sistema y escriba los siguientes comandos. Reemplace *<parameter>* con la información designada.  
  
**Para ejecutar la actualización de Microsoft:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Para informar del estado de Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Vea también  
[Desinstalar las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Desinstalar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
