---
title: Elemento return (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
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
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1c4ce55f4bc63b0011d836ba6e6041f2bd72db85
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene la información devuelta por un [DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md) elemento en respuesta a un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) llamada al método o una [ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento en respuesta a una [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
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
  
  
