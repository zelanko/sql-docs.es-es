---
title: Valor de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2ecaaf902ee1f29700b2d6333bbccd549d9c2193
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062856"
---
# <a name="value-element-xmla"></a>Elemento Value (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene el valor deseado de un [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elemento va a agregar mediante una [insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md) comando, o un [celda](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) elemento actualizará un [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute> <!-- or Cell --!>  
   ...  
   <Value>...</Value>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cualquiera|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [celda](../../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para **atributo** elementos, el **valor** elemento contiene el valor deseado que el miembro debería contener una vez el **insertar** comando se confirma. Para obtener más información acerca de cómo insertar los miembros, vea [Insertar, actualizar y quitar miembros &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
 Para **celda** elementos, el **valor** elemento contiene el valor deseado que la celda debe contener una vez el **UpdateCells** comando se confirma. El valor real almacenado en la tabla de reescritura para esa celda es la diferencia entre el valor original de la celda y el valor deseado de la misma.  
  
 El tipo de datos utilizado por este elemento debería coincidir con el tipo de datos de la celda que se va a estar actualizada.  
  
 Para más información sobre la actualización de celdas, vea [Actualizar celdas &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/updating-cells-xmla.md).  
  
## <a name="see-also"></a>Vea también
 [Elemento CellOrdinal &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/cellordinal-element-xmla.md)   
 [Insertar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento UpdateCells &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
