---
title: Propiedades del servidor (página General) | Microsoft Docs
ms.date: 06/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9c9079baf374b6ab60cf275aaa6551eba5385e79
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712036"
---
# <a name="report-server-properties-general-page"></a>Propiedades del servidor de informes (página General)
  Use esta página para ver o modificar el título usado en el Administrador de informes, habilitar o deshabilitar Mis informes, seleccionar una definición de roles para la seguridad de Mis informes, y habilitar o deshabilitar el control de impresión del cliente.  
  
 **Para abrir esta página:**
 1) Iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) Conéctese a una instancia del servidor de informes.
 3) Haga clic con el botón derecho en el nombre del servidor de informes y seleccione **Propiedades**.  
  
 El modo de servidor determina qué propiedades de servidor se pueden establecer. Si administra un servidor de informes configurado para el modo integrado con SharePoint, no puede habilitar Mis informes o establecer el título de la aplicación para el portal web.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre que aparecerá en la parte superior del portal web. De forma predeterminada, este valor es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. El nombre que especificó solamente aparece en el Administrador de informes.  
  
 **Versión**  
 Esta propiedad es de solo lectura. Especifica la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que está usando.  
  
 **Edición**  
 Esta propiedad es de solo lectura. Especifica la instancia del servidor de informes actual. El Administrador de informes no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ediciones y características admitidas de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
 **Modo de autenticación**  
 Esta propiedad es de solo lectura. Identifica los tipos de solicitudes de autenticación aceptados por la instancia del servidor de informes. Para cambiar el modo de autenticación, tiene que editar el archivo **RSReportServer.config** . Para más información, consulte [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md).  
  
 **Dirección URL**  
 Esta propiedad es de solo lectura. Especifica la dirección URL al servicio web del servidor de informes. Este valor se especifica en la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
 **Habilitar una carpeta Mis informes para cada usuario**  
 Hace que **Mis Informes** esté disponible para los usuarios. Esta opción solo está disponible para los servidores de informes en modo nativo.  
  
 **Seleccione el rol que se aplicará a cada una de las carpetas de Mis informes**  
 Especifique una definición de roles para usarla para la seguridad de Mis informes. La definición de roles identifica el conjunto de tareas que se admiten en cada carpeta Mis informes.  

  
## <a name="see-also"></a>Ver también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Habilitar y deshabilitar Mis informes](../../reporting-services/report-server/enable-and-disable-my-reports.md)   
 [Servidor de informes en Management Studio ayuda F1](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Proteger Mis informes](../../reporting-services/security/secure-my-reports.md)  
  
  

