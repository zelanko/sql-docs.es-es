---
title: "Configurar el Administrador de informes para pasar cookies de autenticaci&#243;n personalizada | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "autenticación [Reporting Services]"
  - "extensiones [Reporting Services], seguridad personalizada"
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 18
---
# Configurar el Administrador de informes para pasar cookies de autenticaci&#243;n personalizada
  Si está utilizando una extensión de autenticación personalizada, debe configurar el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies de autenticación personalizada. De lo contrario, el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] solamente transmitirá cookies por medio de solicitudes HTTP específicas del servidor de informes. Si desea transmitir cookies adicionales, debe modificar el archivo RSReportServer.Config.  
  
## Modificar el archivo RSReportServer.Config  
 Puede habilitar el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies adicionales mediante el servidor de informes si agrega un elemento \<**PassThroughCookies**> a los valores de configuración del [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] del archivo RSReportServer.config. La transmisión de cookies adicionales resulta útil en una solución de autenticación de inicio de sesión único que requiera no solo las cookies de autenticación del servidor de informes, sino también cookies de un sistema de autenticación de otro proveedor.  
  
 Para permitir que se transmitan cookies adicionales mediante solicitudes HTTP al usar el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)], configure los elementos siguientes en el archivo RSReportServer.config:  
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## Vea también  
 [Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)   
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Información general de extensiones de seguridad](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
 [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  