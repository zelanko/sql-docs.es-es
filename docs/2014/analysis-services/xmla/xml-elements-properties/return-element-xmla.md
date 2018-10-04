---
title: Elemento return (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- return Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.return
- http://schemas.microsoft.com/analysisservices/2003/engine#return
- urn:schemas-microsoft-com:xml-analysis#return
helpviewer_keywords:
- return element
ms.assetid: 3cfe8b74-fec3-4987-a74a-5f731444e024
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9484532d235d923dae8b28ab42bd7e4af4523346
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217535"
---
# <a name="return-element-xmla"></a>Elemento return (XMLA)
  Contiene información devuelta por un [DiscoverResponse](../xml-elements-objects-discoverresponse.md) elemento en respuesta a un [Discover](../xml-elements-methods-discover.md) llamada al método o una [ExecuteResponse](../xml-elements-objects-executeresponse.md) elemento en respuesta a una [Execute](../xml-elements-methods-execute.md) llamada al método.  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DiscoverResponse](../xml-elements-objects-discoverresponse.md), [ExecuteResponse](../xml-elements-objects-executeresponse.md)|  
|Antecesor:[DiscoverResponse](../xml-elements-objects-discoverresponse.md)|Secundarios: <br />                        [Raíz](root-element-xmla.md)|  
|Antecesor: <br />                        [ExecuteResponse](../xml-elements-objects-executeresponse.md)|Secundarios: [raíz](root-element-xmla.md) o [resultados](results-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `return` contiene los datos devueltos por los métodos `Discover` y `Execute`. Normalmente, el elemento `return` contiene un único elemento `root` que contiene los datos devueltos por una llamada correcta al método `Discover` o `Execute`, o por una excepción de XML for Analysis (XMLA) devuelta por una llamada al método que no se ha realizado correctamente. Si el método `Execute` contiene un comando `Batch` que realiza varias operaciones, el elemento `return` contiene un elemento `results` que, a su vez, contiene un elemento `root` para cada comando ejecutado correcta o incorrectamente por el comando `Batch`.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
