---
title: Propiedades del servidor (página General) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.general.f1
ms.assetid: 23537d52-4356-450f-a671-5921cef2431f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93365925d412f672b9e8d3e5a9b5f67a850e508a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100013"
---
# <a name="server-properties-general-page"></a>Propiedades del servidor (página General)
  Use esta página para ver o modificar el título usado en el Administrador de informes, habilitar o deshabilitar Mis informes, seleccionar una definición de roles para la seguridad de Mis informes, y habilitar o deshabilitar el control de impresión del cliente.  
  
 Para abrir esta página, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conectarse a una instancia de servidor de informes, haga clic en el nombre del servidor de informes y, a continuación, seleccione **propiedades**.  
  
 El modo de servidor determina qué propiedades de servidor se pueden establecer. Si está administrando un servidor de informes configurado para el modo integrado con SharePoint, no puede habilitar Mis informes o establecer el título de la aplicación para el Administrador de informes.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba un nombre de aplicación que aparece en el Administrador de informes. De forma predeterminada, este valor es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. El nombre que especificó solamente aparece en el Administrador de informes.  
  
 **Versión**  
 Esta propiedad es de solo lectura. Especifica la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que está usando.  
  
 **Edición**  
 Esta propiedad es de solo lectura. Especifica la instancia del servidor de informes actual. El Administrador de informes no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **Modo de autenticación**  
 Esta propiedad es de solo lectura. Identifica los tipos de solicitudes de autenticación aceptados por la instancia del servidor de informes. Para cambiar el modo de autenticación, debe editar el archivo RSReportServer.config. Para más información, consulte [Authentication with the Report Server](../security/authentication-with-the-report-server.md).  
  
 **Dirección URL**  
 Esta propiedad es de solo lectura. Especifica la dirección URL al servicio web del servidor de informes. Este valor se especifica en la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
 **Habilitar una carpeta Mis informes para cada usuario**  
 Hace que Mis Informes esté disponible para los usuarios. Esta opción solo está disponible para los servidores de informes en modo nativo.  
  
 **Seleccione el rol que se aplicará a cada una de las carpetas de Mis informes**  
 Especifique una definición de roles para usarla para la seguridad de Mis informes. La definición de roles identifica el conjunto de tareas que se admiten en cada carpeta Mis informes.  
  
 **Habilitar descarga para el control de impresión de ActiveX client**  
 Establece la propiedad del sistema del servidor de informes `EnableClientPrinting`. Si habilita la impresión del cliente, los usuarios que tienen permisos de administrador local tienen la opción de descargar un control de ActiveX firmado para imprimir informes HTML. Para más información, vea [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar con un servidor de informes en Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Habilitar y deshabilitar Mis informes](../report-server/enable-and-disable-my-reports.md)   
 [Servidor de informes en Management Studio ayuda F1](report-server-in-management-studio-f1-help.md)   
 [Proteger Mis informes](../security/secure-my-reports.md)  
  
  
