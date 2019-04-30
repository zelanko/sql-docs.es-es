---
title: Buscar un informe mediante un acceso URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79c1a291781c5d58b83b05f77ce5ccb952765277
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242442"
---
# <a name="search-a-report-using-url-access"></a>Buscar un informe mediante un acceso URL
  Puede buscar un conjunto concreto de texto en un informe utilizando el acceso URL. Para buscar en un informe, establezca el valor del parámetro *rc:FindString* en la URL igual al texto que desea buscar. Además, utilice los parámetros *rc:StartFind* y *rc:EndFind* para restringir su búsqueda a las páginas determinadas dentro del informe.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de acceso URL busca la primera aparición del texto "Mountain-400" en el informe de ejemplo Catálogo de productos desde la página uno hasta la página cinco:  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>Vea también  
 [Acceso URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referencia de parámetros de acceso URL](url-access-parameter-reference.md)  
  
  
