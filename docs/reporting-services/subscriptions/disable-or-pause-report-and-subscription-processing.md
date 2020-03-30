---
title: Deshabilitar o pausar el procesamiento de informes y suscripciones | Microsoft Docs
ms.date: 06/19/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 228cb40e1c0f40d9525ca83129878d30b722b910
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "68893426"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>Deshabilitar o pausar el procesamiento de informes y suscripciones  
Existen varios enfoques que puede usar para deshabilitar o pausar el procesamiento de informes y suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los enfoques de este artículo comprenden desde deshabilitar una suscripción a interrumpir la conexión del origen de datos. No todos los enfoques son posibles con los dos modos de servidor [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. En las siguientes tablas se resumen los métodos y modos de servidor [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admitidos:  
  
##  <a name="in-this-article"></a><a name="bkmk_top"></a> En este artículo  
  
||Modo de servidor admitido|  
|-|---------------------------|  
|[Habilitar y deshabilitar suscripciones](#bkmk_disable_subscription)|en modo nativo|  
|[Pausar una programación compartida](#bkmk_pause_schedule)|Modo nativo y de SharePoint|  
|[Deshabilitar un origen de datos compartido](#bkmk_disable_shared_datasource)|Modo nativo y de SharePoint|  
|[Modificar asignaciones de roles para impedir el acceso a un informe (modo nativo)](#bkmk_modify_role_assignment)|en modo nativo|  
|[Quitar Administrar permisos de suscripción desde un rol (modo nativo)](#bkmk_remove_manage_subscriptions_permission)|en modo nativo|  
|[Deshabilitar extensiones de entrega](#bkmk_disable_extensions)|Modo nativo y de SharePoint|  
  
##  <a name="enable-and-disable-subscriptions"></a><a name="bkmk_disable_subscription"></a>Habilitar y deshabilitar suscripciones  
  
>[!TIP]  
>Nuevo en SQL 2016 Reporting Services, *Habilitar y deshabilitar suscripciones*. Hay opciones nuevas de interfaz de usuario que le permiten habilitar y deshabilitar rápidamente las suscripciones. Las suscripciones deshabilitadas mantienen sus otras propiedades de configuración, como la programación, y pueden volver a habilitarse fácilmente. También puede habilitar y deshabilitar las suscripciones mediante programación o auditar qué suscripciones están deshabilitadas.  
  
  ![Los botones Habilitar y Deshabilitar de la página Suscripciones ](../../reporting-services/subscriptions/media/disable-or-pause-report-and-subscription-processing/subscription-enable-and-disable-buttons.png)  
  
En el portal web, vaya a la suscripción desde la página **Mis suscripciones** o desde la página **Suscripciones** de una suscripción individual. Seleccione una o más suscripciones y, después, haga clic en el botón Deshabilitar o en el botón Habilitar de la cinta de opciones (consulte la imagen anterior). La columna de estado cambiará a "Deshabilitado" o "Habilitado", respectivamente.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] escribe una fila en el registro [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] al habilitarse o deshabilitarse una suscripción. Por ejemplo, en el archivo de registro del servidor de informes:  
  
 `C:\Program Files\Microsoft SQL Server Reporting Services\SSRS\LogFiles\RSPortal_2019_06_20_00_49_22.log`  
  
 ve filas similares a las siguientes:  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:47:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca disabled at 06/20/2019 01:16:47`  
  
 `RSPortal!subscription!RSPortal.exe!93!06/20/2019-01:16:51:: i INFO: Subscription 2b409d66-d4ea-408a-918c-0f9e41ce49ca enabled at 06/20/2019 01:16:51`  
  
![Contenido relacionado con PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell"): **Use Windows PowerShell para deshabilitar una sola suscripción:** Use el siguiente script de PowerShell para deshabilitar una suscripción específica. Actualice el identificador de la suscripción y el nombre del servidor en el script.  
  
```PS  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid";  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 Puede usar el siguiente script para enumerar todas las suscripciones con sus identificadores. Actualice el nombre del servidor.  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![Contenido relacionado con PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Use Windows PowerShell para mostrar todas las suscripciones deshabilitadas:** use el siguiente script de PowerShell para mostrar todas las suscripciones deshabilitadas del servidor de informes actual de modo nativo. Actualice el nombre del servidor.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![Contenido relacionado con PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Use Windows PowerShell para habilitar todas las suscripciones deshabilitadas:** use el siguiente script de PowerShell para habilitar todas las suscripciones que están deshabilitadas actualmente. Actualice el nombre del servidor.  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![Contenido relacionado con PowerShell](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Use Windows PowerShell para DESHABILITAR todas las suscripciones:** Use el siguiente script de PowerShell para deshabilitar **TODAS** las suscripciones.  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "https://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="pause-a-shared-schedule"></a><a name="bkmk_pause_schedule"></a> Pausar una programación compartida  
 Cuando un informe o una suscripción se ejecutan desde una programación compartida, es posible pausar la programación para evitar el procesamiento. Cualquier proceso de informes o suscripciones controlado por una programación se pospone hasta que se vuelve a reanudar la programación.  
  
-   **Modo SharePoint:** ![Configuración de SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Configuración de SharePoint") En **Configuración del sitio**, seleccione **Administrar programaciones compartidas**. Seleccione la programación y haga clic en **Pausar programaciones seleccionadas**.  
  
-   **Modo nativo:** En el portal web, seleccione el botón **Configuración** ![botón Configuración](media/ssrs-portal-settings-gear.png) en la barra de menús de la parte superior de la pantalla del portal web y seleccione **Configuración del sitio** en el menú desplegable. Seleccione la pestaña **Programaciones** para mostrar la página Programaciones. Active las casillas situadas junto a las programaciones que desea habilitar o deshabilitar y, a continuación, seleccione el botón **Habilitar** o **Deshabilitar** respectivamente para realizar la acción deseada. La columna de estado se actualizará a "Deshabilitado" o "Habilitado", en consecuencia.  
  
##  <a name="disable-a-shared-data-source"></a><a name="bkmk_disable_shared_datasource"></a> Deshabilitar un origen de datos compartido  
 Una de las ventajas de utilizar orígenes de datos compartidos consiste en la posibilidad de deshabilitarlos para evitar la ejecución de un informe o una suscripción controlada por datos. Al deshabilitar un origen de datos compartido, el informe se desconecta de su origen externo. Mientras está deshabilitado, el origen de datos deja de estar disponible para todos los informes y las suscripciones que lo utilizan.  
  
 Tenga en cuenta que el informe se carga igualmente aunque el origen de datos no esté disponible. El informe no contiene datos, pero los usuarios que dispongan de los permisos adecuados pueden tener acceso a las páginas de propiedades, a la configuración de seguridad, al historial del informe y a la información de suscripción asociada al informe.  
  
-   **Modo SharePoint:** para deshabilitar un origen de datos compartido en un servidor de informes en modo de SharePoint, vaya a la biblioteca de documentos que contiene el origen de datos. ![Icono de origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "Icono de origen de datos compartido") Haga clic en el origen de datos y desactive la casilla **Habilitar este origen de datos**.  
  
-   **Modo nativo:** para deshabilitar un origen de datos compartido en un servidor de informes en modo nativo, abra dicho origen de datos desde el portal web y desactive la casilla **Habilitar este origen de datos**.  
  
##  <a name="modify-role-assignments-to-prevent-access-to-a-report-native-mode"></a><a name="bkmk_modify_role_assignment"></a> Modificar asignaciones de roles para impedir el acceso a un informe (modo nativo)  
Una manera de hacer que un informe no esté disponible es eliminar temporalmente la asignación de roles que ofrece acceso al informe en cuestión. Este enfoque es válido para todos los informes, independientemente de cómo se efectúe la conexión al origen de datos. Esta opción afecta solo al informe, no al funcionamiento de otros informes o elementos.  
  
 Para eliminar la asignación de roles, abra la página **Seguridad** del informe desde el portal web. Si el informe hereda la seguridad de otro informe primario, puede seleccionar **Personalizar seguridad** y seleccionar **Confirmar** en el cuadro de diálogo **Editar seguridad del elemento** para crear una directiva de seguridad restrictiva que pase por alto las asignaciones de roles que ofrecen un acceso total (por ejemplo, se puede quitar una asignación de roles que conceda acceso a Todos y mantener la asignación que ofrezca acceso a un grupo reducido de usuarios, como los Administradores).  
  
##  <a name="remove-manage-subscription-permissions-from-role-native-mode"></a><a name="bkmk_remove_manage_subscriptions_permission"></a> Quitar Administrar permisos de suscripción desde un rol (modo nativo)  
 Para evitar que los usuarios puedan crear suscripciones, desactive la tarea **Administrar suscripciones individuales** del rol. Si quita esta tarea, las páginas de Suscripción no estarán disponibles. En el portal web, la página Mis suscripciones aparece vacía (no se puede eliminar), incluso aunque antes contuviese suscripciones. Al quitar tareas relacionadas con una suscripción, se evita que los usuarios creen y modifiquen las suscripciones, pero no se eliminan las suscripciones propiamente dichas. Las suscripciones existentes continúan ejecutándose hasta que las elimine. Para quitar el permiso:  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 
  
2.  Conéctese al servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Expanda el nodo **Seguridad** .  
  
4.  Expanda el nodo **Roles** y seleccione el rol deseado.  
  
5.  Haga clic con el botón derecho en el rol y seleccione **Propiedades**.  
  
6.  Desactive las tareas **Administrar suscripciones individuales** y **Administrar todas las suscripciones**.  
  
7.  Seleccione **Aceptar** para aplicar los cambios.

  
##  <a name="disable-delivery-extensions"></a><a name="bkmk_disable_extensions"></a> Deshabilitar extensiones de entrega  
 Todas las extensiones de entrega instaladas en un servidor de informes están disponibles para cualquier usuario que tenga permiso para crear una suscripción para un informe determinado. Las extensiones de entrega siguientes están disponibles y se configuran automáticamente:  
  
-   Recurso compartido de archivos de Windows  
  
-   Biblioteca de SharePoint (solo disponible desde un sitio de SharePoint integrado con un servidor de informes en el modo integrado de SharePoint)  
  
 Para poder usar la entrega por correo electrónico, debe configurarse previamente. Si no se configura, no estará disponible. Para obtener más información, consulte [Configuración de correo electrónico: modo nativo de Reporting Services (Administrador de configuración)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Si quiere desactivar extensiones concretas, puede quitar las entradas de extensión del archivo **RSReportServer.config** . Para más información, consulte [Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md) y [Configuración de correo electrónico: modo nativo de Reporting Services (Administrador de configuración)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).  
  
 Una vez que quite una extensión de entrega, ya no estará disponible en el portal web o un sitio de SharePoint. Si quita una extensión de entrega, es posible que algunas suscripciones queden inactivas. Asegúrese de eliminar las suscripciones o configurarlas para usar una extensión de entrega diferente antes de quitar una extensión.  
  
## <a name="see-also"></a>Consulte también  
 [Suscripciones y entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Configurar el portal web](../../reporting-services/report-server/configure-web-portal.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [El portal web de un servidor de informes (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [Elementos protegibles](../../reporting-services/security/securable-items.md) 
  
