---
title: La clave de elemento (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Key Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Key
- urn:schemas-microsoft-com:xml-analysis#Key
- microsoft.xml.analysis.key
helpviewer_keywords:
- Key element
ms.assetid: 09d3cd48-49f7-4b58-b8bb-ca75b81bb02f
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 00c7e159e919afe608a9d55c70485592c4b7003d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="key-element-xmla"></a>Elemento Key (XMLA)
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
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Claves](../../../analysis-services/xmla/xml-elements-properties/keys-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El tipo de datos usado por este elemento debería coincidir con el tipo de datos de columna de clave adecuado del atributo especificado. Si los elementos **Key** no se especifican para un elemento **Attribute** primario, los elementos **AttributeName** y **Name** especificados en el elemento **Attribute** primario se usan para identificar el miembro de atributo que se va a modificar.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Attribute &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md)   
 [Elemento AttributeName &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/attributename-element-xmla.md)   
 [Eliminar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Insertar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Elemento KeyColumn &#40; ASSL &#41;](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)   
 [Actualizar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Donde elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

