---
title: Elemento Hierarchies (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Hierarchies Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Hierarchies
helpviewer_keywords:
- Hierarchies element
ms.assetid: dc844eea-869c-4217-b9be-e543a76f5e92
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 1fd20c0c3d9cd521e993bdae1b84ff8fcfb7c40b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchies-element-assl"></a>Elemento Hierarchies (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la colección de elementos [Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) asociada al elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Dimension> <!-- or CubeDimension, PerspectiveDimension -->  
   ...  
   <Hierarchies>  
            <Hierarchy>...</Hierarchy> <!-- parent: Dimension -->  
      <!-- or -->  
      <Hierarchy xsi:type="CubeHierarchy">...</Hierarchy> <!-- parent: CubeDimension -->  
     <!-- or -->  
      <Hierarchy xsi:type="PerspectiveHierarchy">...</Hierarchy> <!-- parent: PerspectiveDimension -->  
   <Hierarchies>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md), [PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Elemento secundario|  
|------------------------|-------------------|  
|[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) de tipo [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)|  
|[Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Jerarquía de](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)|  
|[PerspectiveDimension](../../../analysis-services/scripting/data-type/perspectivedimension-data-type-assl.md)|[Hierarchy](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) de tipo [PerspectiveHierarchy](../../../analysis-services/scripting/data-type/perspectivehierarchy-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.HierarchyCollection>, <xref:Microsoft.AnalysisServices.CubeHierarchyCollection> y <xref:Microsoft.AnalysisServices.PerspectiveHierarchyCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
