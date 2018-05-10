---
title: Configurar el portal web para pasar cookies de autenticación personalizada | Microsoft Docs
ms.custom: ''
ms.date: 04/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: security
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e188a2e036c2bcbfb51aee7dfa0efe5a68879b9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Configurar el portal web para pasar cookies de autenticación personalizada

Si usa una extensión de autenticación personalizada, debe configurar el portal web para transmitir cookies de autenticación personalizada. De lo contrario, el portal web solamente transmitirá cookies por medio de solicitudes HTTP específicas del servidor de informes. Si desea transmitir cookies adicionales, debe modificar el archivo RSReportServer.Config.

## <a name="modifying-the-rsreportserverconfig-file"></a>Modificar el archivo RSReportServer.Config

Puede habilitar el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies adicionales mediante el servidor de informes si agrega un elemento \<**PassThroughCookies**> a los valores de configuración del portal web del archivo RSReportServer.config. La transmisión de cookies adicionales resulta útil en una solución de autenticación de inicio de sesión único que requiera no solo las cookies de autenticación del servidor de informes, sino también cookies de un sistema de autenticación de otro proveedor.

Para permitir que se transmitan cookies adicionales mediante solicitudes HTTP al usar el portal web, configure los elementos siguientes en el archivo RSReportServer.config:
  
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
  
## <a name="see-also"></a>Ver también

[Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)   
[El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Información general de extensiones de seguridad](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
