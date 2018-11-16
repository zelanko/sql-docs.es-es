---
title: Buscar un informe mediante un acceso URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a63f4c1c1ad925ee57def853c76f71ec52f9cb58
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813198"
---
# <a name="search-a-report-using-url-access"></a>Buscar un informe mediante un acceso URL
  Puede buscar un conjunto concreto de texto en un informe utilizando el acceso URL. Para buscar en un informe, establezca el valor del parámetro *rc:FindString* en la URL igual al texto que desea buscar. Además, utilice los parámetros *rc:StartFind* y *rc:EndFind* para restringir su búsqueda a las páginas determinadas dentro del informe.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de acceso URL busca la primera aparición del texto "Mountain-400" en el informe de ejemplo Catálogo de productos desde la página uno hasta la página cinco:  
  
```  
https://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Ver también  
 [Acceso URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](../reporting-services/url-access-parameter-reference.md)  
  
  
