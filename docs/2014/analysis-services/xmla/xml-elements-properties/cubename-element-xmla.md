---
title: Elemento CubeName (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeName
- urn:schemas-microsoft-com:xml-analysis#CubeName
- microsoft.xml.analysis.cubename
helpviewer_keywords:
- CubeName element
ms.assetid: c5c0546e-b9b2-4813-82a9-b028628b88dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 504bf1c6fc83c3c6f4fc92a9ea1220af5933c1da
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178055"
---
# <a name="cubename-element-xmla"></a>Elemento CubeName (XMLA)
  Contiene el nombre del cubo representado por el elemento primario [cubo](cube-element-olapinfo-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube>  
   ...  
   <CubeName>...</CubeName>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](cube-element-olapinfo-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
