---
title: "Especificar la configuración de información de dispositivo en una dirección URL | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 09e1655e7945a459cf9d606d24cf7479ee4fc568
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="specify-device-information-settings-in-a-url"></a>Especificar la configuración de la información del dispositivo en una dirección URL
  Los valores de configuración de información de dispositivos son los parámetros que se pasan a una extensión de representación. Si usa los métodos del servicio web del servidor de informes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para representar un informe, como parámetro de entrada se pasa un elemento XML **DeviceInfo** . Los elementos secundarios del elemento **DeviceInfo** son específicos de la configuración de información de dispositivos de diferentes extensiones de representación. Puede incluir la configuración de información de dispositivos en una dirección URL mediante la cadena de parámetro *rc:tag=value* , donde *tag* es el nombre del elemento de configuración de la información de dispositivos al que se accede. Para más información sobre la configuración de la información de dispositivos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vea [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se establece el formato del informe especificado en JPEG mediante la configuración de información de dispositivos *OutputFormat* de la extensión de representación de la imagen (los saltos de línea se han agregado por legibilidad):  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  
