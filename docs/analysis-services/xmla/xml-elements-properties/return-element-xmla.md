---
title: Elemento return (XMLA) | Documentos de Microsoft
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
- return Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.return
- http://schemas.microsoft.com/analysisservices/2003/engine#return
- urn:schemas-microsoft-com:xml-analysis#return
helpviewer_keywords:
- return element
ms.assetid: 3cfe8b74-fec3-4987-a74a-5f731444e024
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 06b93a7d4c785f8e298a40d6b0accd2ad945b53e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
  Contiene la información devuelta por un [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) elemento en respuesta a un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) llamada al método o una [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento en respuesta a una [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md), [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|  
|Elementos secundarios|Vea la siguiente tabla.|  
  
|Ancestor|Elementos secundarios|  
|--------------|--------------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) o [resultados](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **devolver** elemento contiene los datos devueltos por la **Discover** y **Execute** métodos. Normalmente, el **devolver** elemento contiene un único **raíz** elemento que contiene los datos devueltos por una correcta **Discover** o **Execute** llamada al método o un XML de excepción de Analysis (XMLA) devuelta por una llamada de método incorrecto. Si el **Execute** método contiene un **lote** comando que realiza varias operaciones, el **devolver** elemento contiene un **resultados** elemento que, a su vez, contiene un **raíz** elemento para cada comando ejecutado correcta o incorrectamente por el **lote** comando.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
