---
title: Deshabilitar o pausar el procesamiento de informes y suscripciones | Microsoft Docs
ms.custom: ''
ms.date: 09/29/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: subscriptions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: dfddb0368d8c674c7f0148a395f97088d9143228
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33035532"
---
# <a name="disable-or-pause-report-and-subscription-processing"></a>Deshabilitar o pausar el procesamiento de informes y suscripciones
  Existen varios enfoques que puede usar para deshabilitar o pausar el procesamiento de informes y suscripciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Los enfoques de este tema comprenden desde deshabilitar una suscripción a interrumpir la conexión del origen de datos. No todos los enfoques son posibles con ambos modos de servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . En las tablas siguientes se resumen los métodos y los modos de servidor de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admitidos:  
  
##  <a name="bkmk_top"></a> En este tema  
  
||Modo de servidor admitido|  
|-|---------------------------|  
|[Habilitar y deshabilitar suscripciones](#bkmk_disable_subscription)|en modo nativo|  
|[Pausar una programación compartida](#bkmk_pause_schedule)|Modo nativo y de SharePoint|  
|[Deshabilitar un origen de datos compartido](#bkmk_disable_shared_datasource)|Modo nativo y de SharePoint|  
|[Modificar asignaciones de roles para impedir el acceso a un informe (modo nativo)](#bkmk_modify_role_assignment)|en modo nativo|  
|[Quitar Administrar permisos de suscripción desde un rol (modo nativo)](#bkmk_remove_manage_subscriptions_permission)|en modo nativo|  
|[Deshabilitar extensiones de entrega](#bkmk_disable_extensions)|Modo nativo y de SharePoint|  
  
##  <a name="bkmk_disable_subscription"></a> Habilitar y deshabilitar suscripciones  
  
> [!TIP]  
>  Novedad de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]: **Habilitar y deshabilitar suscripciones**. Hay opciones nuevas de interfaz de usuario que le permiten habilitar y deshabilitar rápidamente las suscripciones. Las suscripciones deshabilitadas mantienen sus otras propiedades de configuración, como la programación, y pueden habilitarse fácilmente. También puede habilitar y deshabilitar las suscripciones mediante programación o auditar qué suscripciones están deshabilitadas.  
  
 ![cinta de suscripción de reporting services](../../reporting-services/subscriptions/media/ssrs-subscription-ribbon.png "cinta de suscripción de reporting services")  
  
 En el Administrador de informes de modo nativo, vaya a la suscripción desde la página **Mis suscripciones** o desde la página **Administrar** de una suscripción individual. Seleccione una o varias suscripciones y luego haga clic en el botón Deshabilitar ![Deshabilitar una suscripción de Reporting Services](../../reporting-services/subscriptions/media/ssrs-disable-subscription.png "Deshabilitar una suscripción de Reporting Services") o Habilitar ![Habilitar una suscripción de Reporting Services](../../reporting-services/subscriptions/media/ssrs-enable-subscription.png "Habilitar una suscripción de Reporting Services") en la cinta. Las suscripciones deshabilitadas se marcan con un icono de advertencia ![Advertencia de estado de una suscripción de Reporting Services](../../reporting-services/subscriptions/media/ssrs-subscription-warning.png "Advertencia de estado de una suscripción de Reporting Services") y el estado se muestra como **Deshabilitado**.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] escribe una fila en el registro de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cuando una suscripción está deshabilitada y otra entrada cuando la suscripción está habilitada. Por ejemplo, en el archivo de registro del servidor de informes:  
  
 `C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__10_16_2014_00_02_18.log`  
  
 ve filas similares a las siguientes:  
  
 `library!ReportServer_0-1!b08!10/16/2014-16:21:14:: i INFO: Call to DisableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934)`  
  
 `library!ReportServer_0-1!2eec!10/16/2014-16:44:18:: i INFO: Call to EnableSubscriptionAction(SubscriptionID=e843bc2b-023e-45a3-ba23-22f9dc9a0934).`  
  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Usar Windows PowerShell para deshabilitar una suscripción única:** use el siguiente script de PowerShell para deshabilitar una suscripción concreta. Actualice el identificador de la suscripción y el nombre del servidor.  
  
```  
#disable specific subscription  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptionID = "subscription guid”;  
$rs2010.DisableSubscription($subscriptionID);  
  
```  
  
 Puede usar el siguiente script para enumerar todas las suscripciones con sus identificadores. Actualice el nombre del servidor.  
  
```  
#list all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME /ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
$subscriptions | select subscriptionid, report, status, path  
  
```  
  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Usar Windows PowerShell para mostrar todas las suscripciones deshabilitadas:** use el siguiente script de PowerShell para mostrar todas las suscripciones deshabilitadas en el servidor de informes actual de modo nativo. Actualice el nombre del servidor.  
  
```  
#list all disabled subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://uetestb03/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
Write-Host "--- Disabled Subscriptions ---";  
Write-Host "----------------------------------- ";  
$subscriptions | Where-Object {$_.Active.DisabledByUserSpecified -and $_.Active.DisabledByUser } | select subscriptionid, report, status, lastexecuted,path | format-table -auto  
```  
  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Usar Windows PowerShell para habilitar todas las suscripciones deshabilitadas:** use el siguiente script de PowerShell para habilitar todas las suscripciones deshabilitadas. Actualice el nombre del servidor.  
  
```  
#enable all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") | Where-Object {$_.status -eq "disabled" } ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.EnableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
  
```  
  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") **Usar Windows PowerShell para deshabilitar todas las suscripciones:** use el siguiente script de PowerShell para deshabilitar **TODAS** las suscripciones.  
  
```  
#DISABLE all subscriptions  
$rs2010 = New-WebServiceProxy -Uri "http://SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/") ;  
ForEach ($subscription in $subscriptions)  
{  
    $rs2010.DisableSubscription($subscription.SubscriptionID);  
    $subscription | select subscriptionid, report, path  
}  
```  
  
##  <a name="bkmk_pause_schedule"></a> Pausar una programación compartida  
 Cuando un informe o una suscripción se ejecutan desde una programación compartida, es posible pausar la programación para evitar el procesamiento. Cualquier proceso de informes o suscripciones controlado por una programación se pospone hasta que se vuelve a reanudar la programación.  
  
-   **Modo de SharePoint:** ![Configuración de SharePoint](../../analysis-services/media/as-sharepoint2013-settings-gear.gif "Configuración de SharePoint") En **Configuración del sitio**, seleccione **Administrar programaciones compartidas**. Seleccione la programación y haga clic en **Pausar programaciones seleccionadas**.  
  
-   **Modo nativo:** En el Administrador de informes, haga clic en **Configuración del sitio**. Seleccione la programación y después haga clic en **Pausar**.  
  
##  <a name="bkmk_disable_shared_datasource"></a> Deshabilitar un origen de datos compartido  
 Una de las ventajas de utilizar orígenes de datos compartidos consiste en la posibilidad de deshabilitarlos para evitar la ejecución de un informe o una suscripción controlada por datos. Al deshabilitar un origen de datos compartido, el informe se desconecta de su origen externo. Mientras está deshabilitado, el origen de datos deja de estar disponible para todos los informes y las suscripciones que lo utilizan.  
  
 Tenga en cuenta que el informe se carga igualmente aunque el origen de datos no esté disponible. El informe no contiene datos, pero los usuarios que dispongan de los permisos adecuados pueden tener acceso a las páginas de propiedades, a la configuración de seguridad, al historial del informe y a la información de suscripción asociada al informe.  
  
-   **Modo de SharePoint:** Para deshabilitar un origen de datos compartido en un servidor de informes en modo de SharePoint, vaya a la biblioteca de documentos que contiene el origen de datos. ![Icono de origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "Icono de origen de datos compartido") Haga clic en el origen de datos y desactive la casilla **Habilitar este origen de datos**.  
  
-   **Modo nativo:** Para deshabilitar un origen de datos compartido en un servidor de informes en modo nativo, abra dicho origen de datos desde el Administrador de informes y desactive la casilla **Habilitar este origen de datos** .  
  
##  <a name="bkmk_modify_role_assignment"></a> Modificar asignaciones de roles para impedir el acceso a un informe (modo nativo)  
 Una manera de hacer que un informe no esté disponible es eliminar temporalmente la asignación de roles que ofrece acceso al informe en cuestión. Este enfoque es válido para todos los informes, independientemente de cómo se efectúe la conexión al origen de datos. Esta opción afecta solo al informe, no al funcionamiento de otros informes o elementos.  
  
 Para eliminar la asignación de roles, abra la página de propiedades Seguridad del informe desde el Administrador de informes. Si el informe hereda la seguridad de otro informe primario, haga clic en **Editar seguridad del elemento** para crear una directiva de seguridad restrictiva que pase por alto las asignaciones de roles que ofrecen un acceso total (por ejemplo, se puede quitar una asignación de roles que conceda acceso a Todos y mantener la asignación que ofrezca acceso a un grupo reducido de usuarios, como los Administradores).  
  
##  <a name="bkmk_remove_manage_subscriptions_permission"></a> Quitar Administrar permisos de suscripción desde un rol (modo nativo)  
 Para evitar que los usuarios puedan crear suscripciones, desactive la tarea **Administrar suscripciones individuales** del rol. Si quita esta tarea, las páginas de Suscripción no estarán disponibles. En el Administrador de informes, la página Mis suscripciones aparece vacía (no se puede eliminar), incluso aunque antes contuviese suscripciones. Al quitar tareas relacionadas con una suscripción, se evita que los usuarios creen y modifiquen las suscripciones, pero no se eliminan las suscripciones propiamente dichas. Las suscripciones existentes continúan ejecutándose hasta que las elimine. Para quitar el permiso:  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
2.  Conéctese al servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Expanda el nodo **Seguridad** .  
  
4.  Seleccione el rol y borre la tarea **Administrar suscripciones individuales** .  
  
##  <a name="bkmk_disable_extensions"></a> Deshabilitar extensiones de entrega  
 Todas las extensiones de entrega instaladas en un servidor de informes están disponibles para cualquier usuario que tenga permiso para crear una suscripción para un informe determinado. Las extensiones de entrega siguientes están disponibles y se configuran automáticamente:  
  
-   Recurso compartido de archivos de Windows  
  
-   Biblioteca de SharePoint (solo disponible desde un sitio de SharePoint integrado con un servidor de informes en el modo integrado de SharePoint)  
  
 Para poder usar la entrega por correo electrónico, debe configurarse previamente. Si no se configura, no estará disponible. Para obtener más información, vea [Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Si quiere desactivar extensiones concretas, puede quitar las entradas de extensión del archivo **RSReportServer.config** . Para obtener más información, vea [Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md) y [Configurar un servidor de informes para la entrega de correo electrónico (Administrador de configuración de SSRS)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Una vez que quite una extensión de entrega, ya no estará disponible en el Administrador de informes o un sitio de SharePoint. Si quita una extensión de entrega, es posible que algunas suscripciones queden inactivas. Asegúrese de eliminar las suscripciones o configurarlas para usar una extensión de entrega diferente antes de quitar una extensión.  
  
## <a name="see-also"></a>Ver también  
 [Suscripciones y entrega &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Configurar el Administrador de informes &#40;modo nativo&#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Página de propiedades de seguridad, elementos &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/351b8503-354f-4b1b-a7ac-f1245d978da0)  
  
  
