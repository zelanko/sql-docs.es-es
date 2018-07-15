---
title: Elemento Update (XMLA) | Microsoft Docs
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
- Update Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Update
- microsoft.xml.analysis.update
- http://schemas.microsoft.com/analysisservices/2003/engine#Update
helpviewer_keywords:
- Update command [XMLA]
ms.assetid: 324dcc16-865d-4d0a-b393-2b06c18ac807
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 75dda4a163ce6551246e11aa9eba6b57fcd9fb25
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283963"
---
# <a name="update-element-xmla"></a>Elemento Update (XMLA)
  Actualiza miembros de atributo de una dimensión.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Update>  
      <Object>...</Object>  
      <MoveWithDescendants>...</MoveWithDescendants>  
      <Attributes>...</Attributes>  
      <Where>...</Where>  
   </Update>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Atributos](../xml-elements-properties/attributes-element-xmla.md), [MoveWithDescendants](../xml-elements-properties/movewithdescendants-element-xmla.md), [objeto](../xml-elements-properties/object-element-dimension-xmla.md), [donde](../xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El comando `Update` mueve los miembros de atributo dentro de una dimensión habilitada para escritura.  
  
 Para obtener más información acerca de cómo actualizar miembros, vea [Insertar, actualizar y quitar miembros &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento DROP &#40;XMLA&#41;](drop-element-xmla.md)   
 [Insertar elemento &#40;XMLA&#41;](insert-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
