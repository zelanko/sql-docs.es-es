---
title: Nombre de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c0686dfbb5949c9b2fe3a20e34824e731369b266
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968887"
---
# <a name="name-element-xmla"></a>Elemento Name (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene el nombre de un miembro de atributo para el elemento primario [atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) o [traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|[Traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para **atributo** elementos, el **nombre** elemento contiene el nombre del miembro de atributo que se pueden insertar ni actualizar durante, respectivamente, la **insertar** o **Actualización** comando.  
  
 Para **traducción** elementos, el **nombre** elemento contiene el título del miembro de atributo, en el idioma especificado por el **lenguaje** elemento primario  **Traducción** objeto. Si el **nombre** elemento no se especifica o contiene una cadena vacía, el valor de la **nombre** (elemento) para el **atributo** elemento que contiene el  **Traducción** se usa el elemento.  
  
## <a name="see-also"></a>Vea también
 [Insertar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento de lenguaje &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
