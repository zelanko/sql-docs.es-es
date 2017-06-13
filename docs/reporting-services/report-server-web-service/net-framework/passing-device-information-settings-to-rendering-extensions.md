---
title: "Pasar la configuración de información de dispositivo para las extensiones de representación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
caps.latest.revision: 47
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: da897abf38fb1c6e89178a9314189890b88eab87
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>Pasar la configuración de información de dispositivo a las extensiones de representación
  En [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], la configuración de información de dispositivos se utiliza para pasar los parámetros de representación a una extensión de representación. La configuración en el servicio web del servidor de informes se pasa como un elemento XML **DeviceInfo** y es procesada por el servidor de informes. Dado que la configuración de información de dispositivos tiene valores predeterminados, se consideran como argumentos opcionales en el proceso de representación. Sin embargo, puede utilizar la configuración de información de dispositivos para personalizar la representación y anular los valores predeterminados proporcionados por el servidor.  
  
 Puede especificar la configuración de información de dispositivos de distintas maneras. Mediante programación, puede utilizar el método Render. Si está teniendo acceso a un informe a través de su URL, puede especificar la información del dispositivo como parámetros URL. También puede modificar la configuración de información de dispositivos en los archivos de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para especificar globalmente los parámetros de representación. Para obtener más información acerca de cómo especificar globalmente los parámetros de representación, vea [personalizar parámetros de extensión de representación en RSReportServer.Config](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).  
  
## <a name="passing-device-information-using-the-render-method"></a>Pasar información del dispositivo utilizando el método Render  
 To pass device information settings to a rendering extension, use the **M:Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@,Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.Warning[]@,System.String[]@)** method. Por ejemplo, la siguiente cadena XML puede pasarse a la <xref:ReportExecution2005.ReportExecutionService.Render%2A> método para crear un fragmento HTML al representar en HTML.  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 Cuando un informe se representa como un fragmento HTML, el contenido del informe se incluye dentro de un elemento TABLE sin el uso del elemento BODY o HTML. Puede utilizar el fragmento HTML para incorporar el informe en un documento HTML existente. Para obtener más información sobre la configuración de información de dispositivo para la salida HTML, vea [HTML Device Information Settings](../../../reporting-services/html-device-information-settings.md).  
  
## <a name="passing-device-information-using-url-access"></a>Pasar información del dispositivo mediante acceso URL  
 También puede pasar la configuración de información de dispositivos a través del acceso URL. La configuración de información de dispositivos se pasa como parámetros URL. La cadena de acceso URL siguiente se puede pasar al servidor de informes para generar un informe representado sin la barra de herramientas del Visor HTML.  
  
```  
http://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 Para obtener más información, consulte [especificar Device Information Settings en una dirección URL](../../../reporting-services/specify-device-information-settings-in-a-url.md).  
  
## <a name="see-also"></a>Vea también  
 [Configuración de la información de dispositivo para representar extensiones &#40; Reporting Services &#41;](../../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
