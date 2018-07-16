---
title: Elemento Parameter (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Parameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parameter
- microsoft.xml.analysis.parameter
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameter
helpviewer_keywords:
- Parameter element
ms.assetid: fe31ac3d-a3e8-4f60-a81a-c43271ddbed4
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 07af3cb2626fb0c6407ce07e0521e665f0d5d556
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245632"
---
# <a name="parameter-element-xmla"></a>Elemento Parameter (XMLA)
  Contiene el nombre y valor de un parámetro utilizados por el método [Execute](../xml-elements-methods-execute.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Parameters>  
...  
   <Parameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </Parameter>  
...  
</Parameters>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Parámetros](parameters-element-xmla.md)|  
|Elementos secundarios|[Name](name-element-parameter-xmla.md), [Value](value-element-parameter-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Alguna parte del código XML para los comandos de Analysis (XMLA), como el comando [Process](../xml-elements-commands/process-element-xmla.md) , puede requerir información adicional. El elemento `Parameter` proporciona un mecanismo para ofrecer información adicional, incluso información en lotes, para un comando XMLA.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
