---
title: "Configurar el Portal Web para pasar Cookies de autenticación personalizada | Documentos de Microsoft"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Configurar el portal web para pasar cookies de autenticación personalizada

Si está utilizando una extensión de autenticación personalizada, debe configurar el portal web para transmitir cookies de autenticación personalizada. En caso contrario, el portal web solamente transmitirá cookies por medio de solicitudes HTTP específicas para el servidor de informes. Si desea transmitir cookies adicionales, debe modificar el archivo RSReportServer.Config.

## <a name="modifying-the-rsreportserverconfig-file"></a>Modificar el archivo RSReportServer.Config

Puede habilitar la [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para transmitir cookies adicionales mediante el servidor de informes mediante la adición de un \< **PassThroughCookies**> elemento en la configuración de la configuración del portal web en el archivo RSReportServer.config. La transmisión de cookies adicionales resulta útil en una solución de autenticación de inicio de sesión único que requiera no solo las cookies de autenticación del servidor de informes, sino también cookies de un sistema de autenticación de otro proveedor.

Para habilitar cookies adicionales para su transmisión a través de las solicitudes HTTP al usar el portal web, configure los elementos siguientes en el archivo RSReportServer.config:
  
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
  
## <a name="see-also"></a>Vea también

[Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)   
[El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Información general de las extensiones de seguridad](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Configurar y administrar un servidor de informes &#40; Modo nativo de SSRS &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
¿Más preguntas? [Pruebe el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
