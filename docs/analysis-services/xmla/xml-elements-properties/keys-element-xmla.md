---
title: Claves de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c8ad15ae719e3d0bd31dccda3271ffccdbeacbfd
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575547"
---
# <a name="keys-element-xmla"></a>Elemento Keys (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de [clave](../../../analysis-services/xmla/xml-elements-properties/key-element-xmla.md) elementos que se usan para identificar las claves de miembro del miembro de atributo representado por el elemento primario [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute>  
   ...  
   <Keys>  
      <Key>...</Key>  
   </Keys>  
   ...  
</Attribute>  
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
|Elementos primarios|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|  
|Elementos secundarios|[Key](../../../analysis-services/xmla/xml-elements-properties/key-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también
 [Elemento DROP &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Insertar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
