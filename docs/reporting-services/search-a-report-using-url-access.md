---
title: Buscar un informe mediante un acceso URL | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7c29c0b4dce06371fc489d8c04f59655057b19a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="search-a-report-using-url-access"></a>Buscar un informe mediante un acceso URL
  Puede buscar un conjunto concreto de texto en un informe utilizando el acceso URL. Para buscar en un informe, establezca el valor del parámetro *rc:FindString* en la URL igual al texto que desea buscar. Además, utilice los parámetros *rc:StartFind* y *rc:EndFind* para restringir su búsqueda a las páginas determinadas dentro del informe.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de acceso URL busca la primera aparición del texto "Mountain-400" en el informe de ejemplo Catálogo de productos desde la página uno hasta la página cinco:  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Ver también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  
