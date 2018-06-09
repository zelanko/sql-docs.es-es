---
title: La clave de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bea00c5b5fdff010d667db19ef3af28284ce3ed9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575787"
---
# <a name="key-element-xmla"></a>Elemento Key (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene un valor de clave de miembro para un miembro de atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Keys>  
   ...  
   <Key>...</Key>  
   ...  
</Keys>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cualquiera|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Claves](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El tipo de datos usado por este elemento debería coincidir con el tipo de datos de columna de clave adecuado del atributo especificado. Si los elementos **Key** no se especifican para un elemento **Attribute** primario, los elementos **AttributeName** y **Name** especificados en el elemento **Attribute** primario se usan para identificar el miembro de atributo que se va a modificar.  
  
## <a name="see-also"></a>Vea también
 [Atributo de elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [Elemento AttributeName &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [Elemento DROP &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Insertar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento KeyColumn &#40;ASSL&#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [Actualizar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Donde elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
