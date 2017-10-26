---
title: Elemento RestrictionList (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RestrictionList Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df82fa9bb12094ae01535977f10f26622cbac6b2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="restrictionlist-element-xmla"></a>Elemento RestrictionList (XMLA)
  Contiene una colección de columnas de restricción y valores usados por el método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Restricciones](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|Elementos secundarios|Columnas de restricción y valores (vea Comentarios).|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **RestrictionList** contiene una colección de columnas de restricción en la que los datos devueltos por el método **Discover** se pueden filtrar. Cada columna de restricción del elemento **RestrictionList** está definida por un elemento XML diferente. El valor de la columna de restricción son los datos que contienen el elemento XML y el nombre de la columna de restricción se corresponde al nombre del elemento XML.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

