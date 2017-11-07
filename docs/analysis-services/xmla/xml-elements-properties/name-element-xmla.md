---
title: Nombre de elemento (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Name Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5251f22e39932f49fa4c512b8c5b76a2bf0e7af9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="name-element-xmla"></a>Elemento Name (XMLA)
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
|Cardinalidad|Vea la siguiente tabla.|  
  
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
 [Insertar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento del lenguaje &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/language-element-xmla.md)   
 [Actualizar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

