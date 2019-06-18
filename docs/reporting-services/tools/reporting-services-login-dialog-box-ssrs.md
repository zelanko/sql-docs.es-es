---
title: Inicio de sesión de Reporting Services (cuadro de diálogo de SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25d2741a8449875852c733aa763322011834a6b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581279"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Inicio de sesión de Reporting Services (cuadro de diálogo de SSRS)
  Utilice el cuadro de diálogo **Inicio de sesión de Reporting Services** para proporcionar credenciales para publicar informes en el servidor de informes.  
  
-   **Nota** Si es la primera vez que publica un informe en un servidor de informes desde que ha establecido la propiedad de implementación **TargetServerURL** para un proyecto, compruebe que en el nombre del servidor que ha especificado se incluye **server** y no **reports**. Por ejemplo, `https://localhost/reportserver`, y no a `https://localhost/reports`. La consecuencia indirecta de especificar el directorio `reports` del servidor local en lugar del directorio `reportserver` es la apertura de este cuadro de diálogo. Para más información sobre cómo establecer **TargetServerURL**, vea [Establecer propiedades de implementación&#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opciones  
 **Server**  
 Muestra el nombre del servidor de informes. Por ejemplo, `https://localhost/reportserver`. Si los servidores de informes usan un puerto distinto del predeterminado, el puerto 80, incluya el número de puerto. Por ejemplo, `https://localhost:81/reportserver`.  
  
 **User name**  
 Escriba el nombre de usuario con el que iniciar sesión en el servicio web.  
  
 **Contraseña**  
 Escriba la contraseña con la que iniciar sesión en el servicio web.  
  
## <a name="see-also"></a>Consulte también  
 [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Diseñador de informes (Ayuda F1)](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
