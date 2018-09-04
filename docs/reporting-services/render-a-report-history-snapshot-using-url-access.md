---
title: Representar instantáneas del historial de informes mediante acceso URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 44de81b48604356761ed855f4b765af60cb75103
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43279267"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>Representar instantáneas del historial de informes mediante acceso URL
  Puede representar un informe basado en una instantánea del historial de informes si proporciona el parámetro *rs:Snapshot* y establece su valor en un identificador de instantánea válido. El valor del parámetro está en el formato AAAA-MM-DDTHH:MM:SS, según el estándar 8601 de la Organización internacional de normalización (ISO).  
  
 Si omite este parámetro, el informe se representa según la configuración de la ejecución del informe y de la administración de la memoria caché del servidor de informes. Para obtener más información sobre la ejecución del informe, vea [Establecer las propiedades del procesamiento de informes](../reporting-services/report-server/set-report-processing-properties.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra una dirección URL que recupera una instantánea del historial de informes:  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>Ver también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  
