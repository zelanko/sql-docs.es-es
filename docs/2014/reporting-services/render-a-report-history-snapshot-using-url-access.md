---
title: Representar instantáneas del historial de informes mediante acceso URL | Microsoft Docs
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
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
caps.latest.revision: 32
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b065fa70d102ff86c25aa0fffb78cfa4993cd284
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272581"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>Representar instantáneas del historial de informes mediante acceso URL
  Puede representar un informe basado en una instantánea del historial de informes si proporciona el parámetro *rs:Snapshot* y establece su valor en un identificador de instantánea válido. El valor del parámetro está en el formato AAAA-MM-DDTHH:MM:SS, según el estándar 8601 de la Organización internacional de normalización (ISO).  
  
 Si omite este parámetro, el informe se representa según la configuración de la ejecución del informe y de la administración de la memoria caché del servidor de informes. Para obtener más información acerca de la ejecución de informes, vea [establecer propiedades de procesamiento de informes](report-server/set-report-processing-properties.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra una dirección URL que recupera una instantánea del historial de informes:  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
  
