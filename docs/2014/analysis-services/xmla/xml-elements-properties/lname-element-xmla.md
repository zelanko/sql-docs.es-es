---
title: Elemento LName (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#LName
- http://schemas.microsoft.com/analysisservices/2003/engine#LName
- microsoft.xml.analysis.lname
helpviewer_keywords:
- LName element
ms.assetid: 2c8c2fa9-cb2d-44ea-b253-5e6ff61f1b66
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ba25e2c379c4049e34e7586e0574332720403c9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168385"
---
# <a name="lname-element-xmla"></a>Elemento LName (XMLA)
  Contiene información acerca de los nombres de nivel únicos para el elemento primario [HierarchyInfo](hierarchyinfo-element-xmla.md) o [miembro](member-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LName>...</LName>  
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
 Para los elementos `HierarchyInfo`, este elemento contiene el nombre de la propiedad que proporciona los nombres de nivel únicos de la jerarquía. El valor es equivalente a la propiedad LEVEL_UNIQUE_NAME definida para conjuntos de filas de ejes en OLE DB para la especificación de OLAP.  
  
 Para los elementos `Member`, este elemento contiene el nombre único del nivel en la jerarquía que contiene el miembro representado por el elemento `Member` primario.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
