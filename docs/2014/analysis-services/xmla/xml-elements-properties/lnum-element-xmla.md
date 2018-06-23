---
title: Elemento LNum (XMLA) | Documentos de Microsoft
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
- LNum Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.lnum
- urn:schemas-microsoft-com:xml-analysis#LNum
- http://schemas.microsoft.com/analysisservices/2003/engine#LNum
helpviewer_keywords:
- LNum element
ms.assetid: 7b9cc143-0c5e-4a8c-a288-8921bfcfd103
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: affdefb04b94d863faa9a9fb6a9eed8ea5b07606
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103151"
---
# <a name="lnum-element-xmla"></a>Elemento LNum (XMLA)
  Contiene información sobre las posiciones ordinales de nivel para el elemento primario [HierarchyInfo](hierarchyinfo-element-xmla.md) o [miembro](member-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LNum>...</LNum>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|INT|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[HierarchyInfo](hierarchyinfo-element-xmla.md), [Member](member-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para los elementos `HierarchyInfo`, el elemento `LNum` contiene el nombre de la propiedad que proporciona las posiciones ordinales de nivel de la jerarquía. El valor es equivalente a la propiedad LEVEL_NUMBER definida para conjuntos de filas de ejes en OLE DB para la especificación de OLAP.  
  
 Para `Member` elementos, el `LNum` elemento contiene la posición ordinal basado en cero, desde el nivel raíz de la jerarquía del miembro representado por el elemento primario [miembro](member-element-xmla.md) elemento. Un valor de cero representa el nivel de raíz de la jerarquía.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  