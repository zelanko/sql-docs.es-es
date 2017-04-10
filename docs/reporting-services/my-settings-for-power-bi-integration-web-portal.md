---
title: "La configuraci&#243;n de la integraci&#243;n de Power BI (portal web) | Microsoft Docs"
ms.date: "05/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "pbi"
  - "power bi"
  - "power bi integration"
ms.assetid: 85c2fac7-80bf-45b7-8654-764b5f5231f5
caps.latest.revision: 15
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 15
---
# La configuraci&#243;n de la integraci&#243;n de Power BI (portal web)
  Los usuarios individuales usan la página **My Settings** (Mi configuración) del [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar los inicios de sesión con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Al seguir los pasos para anclar un elemento de informe, automáticamente se le pedirá que inicie sesión.  Pero puede usar la página **My Settings** (Mi configuración) si necesita iniciar sesión manualmente o si necesita cerrarla.  Si no ve la opción de menú **My Settings** (Mi configuración), se deberá a que el servidor de informes aún no se ha integrado con  [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  Para obtener más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
## Por qué iniciar sesión  
 Al iniciar la sesión, establece una relación entre la cuenta de usuario de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y la cuenta de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  El inicio de sesión crea un token de seguridad que preserva un buen estado durante 90 días. Si el token expira y tiene elementos anclados a Power BI, verá una notificación.  
   
 ![ssRS_WebPortal_PowerBI_Notification](../reporting-services/media/ssrs-webportal-powerbi-notification.png)    
   
Los iconos de los paneles de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] no se actualizarán hasta que vuelva a iniciar sesión a través de la página **My Settings** (Mi configuración).  
  
![ssRS_WebPortal_PowerBI_SignIn_Again](../reporting-services/media/ssrs-webportal-powerbi-signin-again.png)  
  
Una vez que haya iniciado sesión, se creará un token de seguridad.  Los iconos del panel empezarán a actualizarse en los programas configurados anteriormente.  
  
## Vea también  
 [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Anclado de elementos de Reporting Services en panales de Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)   
 [Paneles en Power BI](https://support.powerbi.com/knowledgebase/articles/424868-dashboards-in-power-bi)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
