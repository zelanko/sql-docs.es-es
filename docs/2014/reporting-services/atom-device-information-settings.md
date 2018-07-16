---
title: Configuración de la información del dispositivo ATOM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c4d0f85da3c3762d32b8a59a34e073e9f14736a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321886"
---
# <a name="atom-device-information-settings"></a>Configuración de la información del dispositivo ATOM
  La configuración de información de dispositivo para la extensión de representación Atom admite el envío de un nombre de una fuente Atom y la codificación de caracteres que se usará.  
  
 En la siguiente tabla se enumera la configuración de información de dispositivo para la representación en un documento de servicio de datos.  
  
|Configuración|Valor|  
|-------------|-----------|  
|`DataFeed`|Si se especifica, representa la fuente Atom que corresponde al nombre de fuente proporcionado en esta configuración. De lo contrario, representa el documento de servicio Atom para el informe. El identificador único generado automáticamente de la fuente de distribución de datos. Este valor se usa internamente y no se debe cambiar.|  
|**Codificación**|Nombre del organismo Internet Assigned Numbers Authority (IANA) de una codificación de caracteres que es compatible con .NET Framework. El valor predeterminado es `UTF-8`. Entre los ejemplos de otros valores se incluyen ASCII, UTF-7 y UTF-16.|  
  
## <a name="see-also"></a>Vea también  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Pasar la configuración de información de dispositivo a las extensiones de representación](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Personalizar los parámetros de extensión de representación en RSReportServer.Config](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Referencia técnica &#40;SSRS&#41;](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
