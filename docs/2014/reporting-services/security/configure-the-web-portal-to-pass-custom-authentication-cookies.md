---
title: Configurar el Administrador de informes para pasar Cookies de autenticación personalizada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6c77560c134abf9f255837da71a079506fa0f145
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137015"
---
# <a name="configure-report-manager-to-pass-custom-authentication-cookies"></a>Configurar el Administrador de informes para pasar cookies de autenticación personalizada
  Si está utilizando una extensión de autenticación personalizada, debe configurar el Administrador de informes para transmitir cookies de autenticación personalizada. De lo contrario, el Administrador de informes solamente transmitirá cookies por medio de solicitudes HTTP específicas del servidor de informes. Si desea transmitir cookies adicionales, debe modificar el archivo RSReportServer.Config.  
  
## <a name="modifying-the-rsreportserverconfig-file"></a>Modificar el archivo RSReportServer.Config  
 Puede permitir que el Administrador de informes para transmitir cookies adicionales mediante el servidor de informes si agrega un <`PassThroughCookies`> elemento a los valores de configuración del Administrador de informes en el archivo RSReportServer.config. La transmisión de cookies adicionales resulta útil en una solución de autenticación de inicio de sesión único que requiera no solo las cookies de autenticación del servidor de informes, sino también cookies de un sistema de autenticación de otro proveedor.  
  
 Para permitir que se transmitan cookies adicionales mediante solicitudes HTTP al usar el Administrador de informes, configure los elementos siguientes en el archivo RSReportServer.config:  
  
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
 [Autenticación con el servidor de informes](authentication-with-the-report-server.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Introducción a las extensiones de seguridad](../extensions/security-extension/security-extensions-overview.md)   
 [Configurar y administrar un servidor de informes &#40;modo nativo de SSRS&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
  
  
