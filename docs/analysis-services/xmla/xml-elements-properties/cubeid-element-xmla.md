---
title: Elemento CubeID (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CubeID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cubeid
- urn:schemas-microsoft-com:xml-analysis#CubeID
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeID
helpviewer_keywords:
- CubeID element
ms.assetid: 9dba605a-c45e-4730-827b-b7c55c8110da
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89b16593efe219d0fea6f0d09a0e431a7bab7bd6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cubeid-element-xmla"></a>Elemento CubeID (XMLA)
  Identifica un cubo dentro de un elemento primario que contiene una referencia de objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <CubeID>...</CubeID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|Vea la siguiente tabla.|  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|[Destino](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|Todos los demás|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md), [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md), [Target](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

