---
title: Elemento RestrictionList (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- RestrictionList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords:
- RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 081722ea3a5bf001b22f8c193cd5530a37809e15
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197678"
---
# <a name="restrictionlist-element-xmla"></a>Elemento RestrictionList (XMLA)
  Contiene una colección de columnas de restricción y valores usados por el método [Discover](../xml-elements-methods-discover.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Restricciones](restrictions-element-xmla.md)|  
|Elementos secundarios|Columnas de restricción y valores (vea Comentarios).|  
  
## <a name="remarks"></a>Notas  
 El elemento `RestrictionList` contiene una colección de columnas de restricción en la que los datos devueltos por el método `Discover` se pueden filtrar. Cada columna de restricción del elemento `RestrictionList` está definida por un elemento XML diferente. El valor de la columna de restricción son los datos que contienen el elemento XML y el nombre de la columna de restricción se corresponde al nombre del elemento XML.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  