---
title: Nombre de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f19696ae5eea630a6fe879b603b72c4e955b1ac
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
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
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|[Traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributo](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md), [traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para **atributo** elementos, el **nombre** elemento contiene el nombre del miembro de atributo que se pueden insertar ni actualizar durante, respectivamente, la **insertar** o **Actualización** comando.  
  
 Para **traducción** elementos, el **nombre** elemento contiene el título del miembro de atributo, en el idioma especificado por el **lenguaje** elemento del elemento primario  **Traducción** objeto. Si el **nombre** elemento no se especifica o contiene una cadena vacía, el valor de la **nombre** (elemento) para la **atributo** elemento que contiene el  **Traducción** elemento se utiliza.  
  
## <a name="see-also"></a>Vea también  
 [Insertar elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento del lenguaje &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [Actualizar elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
