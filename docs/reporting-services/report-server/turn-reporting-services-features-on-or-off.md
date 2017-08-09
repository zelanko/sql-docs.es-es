---
title: "Activar características de Reporting Services o desactivar | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a9cb113f44e01052d03fc5354c2cff6da4afb460
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="turn-reporting-services-features-on-or-off"></a>Activar o desactivar las características de Reporting Services
  Puede desactivar características del servidor de informes que no use como parte de una estrategia de bloqueo para reducir la superficie de ataque de un servidor de informes de producción. En la mayoría de los casos, le interesará ejecutar las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] simultáneamente para poder hacer uso de toda la funcionalidad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sin embargo, dependiendo del modelo de implementación, puede deshabilitar aquellas características que no necesite. Por ejemplo, si todo el procesamiento de informes está configurado como operaciones programadas, puede habilitar solo el procesamiento en segundo plano. Del mismo modo, puede ejecutar simplemente el servicio web del servidor de informes si solo desea informes a petición e interactivos.  
  
 En los procedimientos de este tema, se muestra cómo desactivar características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo. Las características se pueden configurar de varias maneras: editando directamente el archivo `RsReportServer.config` o con la faceta **Configuración de área expuesta para Reporting Services** de la administración basada en directivas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Use los vínculos para buscar el procedimiento o los procedimientos en los que se explica cómo activar o desactivar una característica:  
  
-   [servicio web del servidor de informes](#RSWebSvc)  
  
-   [Eventos y procesamiento programados](#Sched)  
  
-   [Portal Web](#WebPortal)  
  
-   [Generador de informes](#ReportBuilder)  
  
-   [Seguridad integrada de Windows para los orígenes de datos de informes](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Report Server Web Service  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>Para activar o desactivar el servicio web del servidor de informes editando la configuración  
  
1.  Abra el archivo `RsReportServer.config` en un editor de texto. Para obtener más información, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para activar el servicio web del servidor de informes, establezca **IsWebServiceEnabled** en **true**:  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  Para desactivar el servicio web del servidor de informes, establezca **IsWebServiceEnabled** en **false**:  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  Guarde los cambios y, a continuación, cierre el archivo.  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>Para activar o desactivar el servicio web del servidor de informes con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que desea configurar.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nodo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , seleccione **Directivas**y, después, haga clic en **Facetas**.  
  
3.  En la lista **Faceta** , seleccione **Configuración de área expuesta para Reporting Services**.  
  
4.  En **Propiedades de faceta**:  
  
    -   Para activar el servicio web del servidor de informes, establezca **WebServiceAndHTTPAccessEnabled** en **True**.  
  
    -   Para desactivar el servicio web del servidor de informes, establezca **WebServiceAndHTTPAccessEnabled** en **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> Eventos programados y entrega programada  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>Para activar o desactivar los eventos programados y la entrega programada editando la configuración  
  
1.  Abra el archivo RsReportServer.config en un editor de texto. Para obtener más información, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Para activar el procesamiento y la entrega de informes programados, establezca **IsSchedulingService**, **IsNotificationService**e **IsEventService** en **true**:  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  Para desactivar el procesamiento y la entrega de informes programados, establezca **IsSchedulingService**, **IsNotificationService**e **IsEventService** en **false**:  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  Guarde los cambios y, a continuación, cierre el archivo.  
  
> [!NOTE]  
>  No puede desactivar completamente ningún procesamiento en segundo plano porque proporciona la funcionalidad de mantenimiento de las bases de datos que se requiere para las operaciones de servidor.  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-using-sql-server-management-studio"></a>Para activar o desactivar los eventos programados y la entrega programada con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que desea configurar.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nodo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , seleccione **Directivas**y, después, haga clic en **Facetas**.  
  
3.  En la lista **Faceta** , seleccione **Configuración de área expuesta para Reporting Services**.  
  
4.  En **Propiedades de faceta**:  
  
    -   Para activar los eventos programados y la entrega programada, establezca **ScheduleEventsAndReportDeliveryEnabled** en **True**.  
  
    -   Para desactivar los eventos programados y la entrega programada, establezca **ScheduleEventsAndReportDeliveryEnabled** en **False**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  No puede desactivar completamente ningún procesamiento en segundo plano porque proporciona la funcionalidad de mantenimiento de las bases de datos que se requiere para las operaciones de servidor.  
  
##  <a name="WebPortal"></a>Portal Web
  
En versiones anteriores, se podía deshabilitar el Administrador de informes estableciendo **IsReportManagerEnabled** en false. **IsReportManagerEnabled** ha quedado obsoleta en SQL Server 2016 Reporting Services actualización acumulativa 2. Siempre se habilitará el portal web.
  
##  <a name="ReportBuilder"></a> Generador de informes  
  
#### <a name="to-turn-on-or-off-report-builder-by-using-sql-server-management-studio"></a>Para activar o desactivar el Generador de informes con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que desea configurar.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nodo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y, después, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del servidor** , en **Seleccionar una página**, haga clic en **Seguridad**.  
  
    -   Para activar el Generador de informes, seleccione la opción **Habilitar ejecuciones de notificaciones ad hoc** .  
  
    -   Para desactivar el Generador de informes, anule la selección de la opción **Habilitar ejecuciones de notificaciones ad hoc** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Seguridad integrada de Windows  
  
#### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>Para activar o desactivar la seguridad integrada de Windows con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que desea configurar.  
  
2.  En el Explorador de objetos, haga clic con el botón derecho en el nodo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y, después, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades del servidor** , en **Seleccionar una página**, haga clic en **Seguridad**.  
  
    -   Para activar la seguridad integrada de Windows, seleccione la opción **Habilitar la seguridad integrada de Windows para los orígenes de datos de informes** .  
  
    -   Para desactivar la seguridad integrada de Windows, anule la selección de la opción **Habilitar la seguridad integrada de Windows para los orígenes de datos de informes** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services (Modo nativo de SSRS)](http://msdn.microsoft.com/en-us/63519ef4-e68a-42fb-9cf7-31228ea4e434)  
 ¿Más preguntas? [Pruebe el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  

