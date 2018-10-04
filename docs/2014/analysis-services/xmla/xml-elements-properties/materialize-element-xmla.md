---
title: Elemento Materialize (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Materialize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.materialize
- http://schemas.microsoft.com/analysisservices/2003/engine#Materialize
- urn:schemas-microsoft-com:xml-analysis#Materialize
helpviewer_keywords:
- Materialize element
ms.assetid: cda19474-7170-4b0e-b0ea-297ce5128112
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76eda53c13b49b9e4f4bc2e4b40e9f169f31841a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157375"
---
# <a name="materialize-element-xmla"></a>Elemento Materialize (XMLA)
  Especifica si se deben materializar las agregaciones diseñadas por el comando [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Materialize>...</Materialize>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|False|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
