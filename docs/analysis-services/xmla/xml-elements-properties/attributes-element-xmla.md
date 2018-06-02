---
title: Atributos de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3dd4d8f56d59eecc61c164e76fe76b776797af0f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577767"
---
# <a name="attributes-element-xmla"></a>Elemento Attributes (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de elementos [Attribute](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) utilizada por los comandos primarios [Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md) o [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) , o por el elemento primario [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Insert > <!-- or one of the elements listed below in the Element relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
   </Attributes>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [Where](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|  
|Elementos secundarios|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
