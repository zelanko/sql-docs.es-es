---
title: Caption (XMLA) del elemento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Caption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Caption
- http://schemas.microsoft.com/analysisservices/2003/engine#Caption
- microsoft.xml.analysis.caption
helpviewer_keywords:
- Caption element
ms.assetid: 3d10ee68-98ab-4da0-a409-800dea2f1c32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4899f19b8a3986e2063d2979ce84c0a0d52d0d02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201485"
---
# <a name="caption-element-xmla"></a>Elemento Caption (XMLA)
  Contiene información sobre el título del elemento primario [HierarchyInfo](hierarchyinfo-element-xmla.md) o [miembro](member-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <Caption>...</Caption>  
   ...  
</HierarchyInfo>  
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
|Elementos primarios|[HierarchyInfo](hierarchyinfo-element-xmla.md), [Member](member-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Para los elementos `HierarchyInfo`, el elemento `Caption` contiene el nombre de la propiedad que proporciona los títulos de miembros de la jerarquía. El valor es equivalente a la propiedad MEMBER_CAPTION definida para conjuntos de filas de ejes en OLE DB para la especificación de OLAP.  
  
 Para los elementos `Member`, el elemento `Caption` contiene el título del elemento `Member` primario en el lenguaje especificado para la sesión de XML for Analysis (XMLA). Si no está disponible ningún título, este elemento contiene el nombre único del miembro.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
