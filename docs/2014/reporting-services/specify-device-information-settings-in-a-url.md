---
title: Especificar la configuración de la información del dispositivo en una dirección URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], URLs
- URL access [Reporting Services], device information settings
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a77fe212fc4637c384a8328aa1094db91b9a8d11
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255577"
---
# <a name="specify-device-information-settings-in-a-url"></a>Especificar la configuración de la información del dispositivo en una dirección URL
  Los valores de configuración de información de dispositivos son los parámetros que se pasan a una extensión de representación. Si utiliza los métodos del servicio web del servidor de informes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para representar un informe, como parámetro de entrada se pasa un elemento XML `DeviceInfo`. Los elementos secundarios de la `DeviceInfo` elemento son específicos de la configuración de información de dispositivos de diferentes extensiones de representación. Puede incluir la configuración de información de dispositivos en una dirección URL mediante la cadena de parámetro *rc:tag=value* , donde *tag* es el nombre del elemento de configuración de la información de dispositivos al que se accede. Para obtener más información sobre la configuración de la información de dispositivo en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se establece el formato del informe especificado en JPEG mediante la configuración de información de dispositivos *OutputFormat* de la extensión de representación de la imagen (los saltos de línea se han agregado por legibilidad):  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
  
