---
title: Elemento UnaryOperator (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UnaryOperator Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#UnaryOperator
- urn:schemas-microsoft-com:xml-analysis#UnaryOperator
- microsoft.xml.analysis.unaryoperator
helpviewer_keywords:
- UnaryOperator element
ms.assetid: 4dc9cfbe-6f8b-42bc-8d3a-42f48ca5d299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb3c90fe9387d0f7eb7f5ae24fbad185f15bd1d2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225235"
---
# <a name="unaryoperator-element-xmla"></a>Elemento UnaryOperator (XMLA)
  Contiene el operador unario para un miembro de atributo representado por el elemento primario [atributo](attribute-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute>  
   ...  
   <UnaryOperator>...</UnaryOperator>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributo](attribute-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `UnaryOperator` contiene una expresión de Expresiones multidimensionales (MDX) que define el operador unario del miembro de atributo definido por el elemento primario `Attribute`.  
  
 Para obtener más información sobre las expresiones MDX, vea [expresiones &#40;MDX&#41;](/sql/mdx/expressions-mdx).  
  
## <a name="see-also"></a>Vea también  
 [Insertar elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
