---
title: Configuración de la información del dispositivo ATOM | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5f5c75583542dd7f2bc62b6de5da2fb457a90296
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33014012"
---
# <a name="atom-device-information-settings"></a>Configuración de la información del dispositivo ATOM
  La configuración de información de dispositivo para la extensión de representación Atom admite el envío de un nombre de una fuente Atom y la codificación de caracteres que se usará.  
  
 En la siguiente tabla se enumera la configuración de información de dispositivo para la representación en un documento de servicio de datos.  
  
|Configuración|Valor|  
|-------------|-----------|  
|**DataFeed**|Si se especifica, representa la fuente Atom que corresponde al nombre de fuente proporcionado en esta configuración. De lo contrario, representa el documento de servicio Atom para el informe. El identificador único generado automáticamente de la fuente de distribución de datos. Este valor se usa internamente y no se debe cambiar.|  
|**Codificación**|Nombre del organismo Internet Assigned Numbers Authority (IANA) de una codificación de caracteres que es compatible con .NET Framework. El valor predeterminado es **UTF-8**. Entre los ejemplos de otros valores se incluyen ASCII, UTF-7 y UTF-16.|  
  
## <a name="see-also"></a>Ver también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
