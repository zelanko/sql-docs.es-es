---
title: Elemento return (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4808372fbf80b2b3a79bc11e3f2423511eb717be
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192413"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DiscoverResponse](../xml-elements-objects-discoverresponse.md), [ExecuteResponse](../xml-elements-objects-executeresponse.md)|  
|Antecesor:[DiscoverResponse](../xml-elements-objects-discoverresponse.md)|Secundarios: <br />                        [raíz](root-element-xmla.md)|  
|Antecesor: <br />                        [ExecuteResponse](../xml-elements-objects-executeresponse.md)|Secundarios: [raíz](root-element-xmla.md) o [resultados](results-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento `return` contiene los datos devueltos por los métodos `Discover` y `Execute`. Normalmente, el elemento `return` contiene un único elemento `root` que contiene los datos devueltos por una llamada correcta al método `Discover` o `Execute`, o por una excepción de XML for Analysis (XMLA) devuelta por una llamada al método que no se ha realizado correctamente. Si el método `Execute` contiene un comando `Batch` que realiza varias operaciones, el elemento `return` contiene un elemento `results` que, a su vez, contiene un elemento `root` para cada comando ejecutado correcta o incorrectamente por el comando `Batch`.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
