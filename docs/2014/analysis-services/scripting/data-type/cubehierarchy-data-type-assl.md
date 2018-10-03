---
title: Tipo de datos CubeHierarchy (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CubeHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeHierarchy
helpviewer_keywords:
- CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ba39d031f8760a82232f4f276c46d04101cc6438
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209655"
---
# <a name="cubehierarchy-data-type-assl"></a>Tipo de datos CubeHierarchy (ASSL)
  Define un tipo de datos primitivo que representa información sobre un [jerarquía](../objects/hierarchy-element-assl.md) elemento en un [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [habilitado](../properties/enabled-element-assl.md), [HierarchyID](../properties/id-element-assl.md), [nombre](../properties/name-element-assl.md), [OptimizedState](../properties/state-element-assl.md), [Visible](../properties/visible-element-assl.md)|  
|Elementos derivados|[Jerarquía](../objects/hierarchy-element-assl.md) ([jerarquías](../collections/hierarchies-element-assl.md) colección de [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 Este tipo de datos no tiene ninguna restricción y se puede usar en cualquier modo de implementación (0-Multidimensional y minería de datos, 1-SharePoint y 2-Tabular).  
  
 En [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)], *habilitado* propiedad no puede establecerse en `False` para *CubeHierarchy*.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubeHierarchy>.  
  
## <a name="see-also"></a>Vea también  
 [Método Discover &#40;XMLA&#41;](../../xmla/xml-elements-methods-discover.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
