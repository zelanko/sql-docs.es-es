---
title: Elemento Description (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Description Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Description
helpviewer_keywords:
- Description element
ms.assetid: 34d67e7c-e79a-429b-8cc3-6ca13b9cf9c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 19a041d81646361d1f6eefb96604829ec1928032
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126135"
---
# <a name="description-element-assl"></a>Elemento Description (ASSL)
  Contiene la descripción del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Description>...</Description>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acción](../objects/action-element-assl.md), [agregación](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [ensamblado](../objects/assembly-element-assl.md), [AttributePermission](../objects/attributepermission-element-assl.md), [ CalculationProperty](../objects/calculationproperty-element-assl.md), [CellPermission](../objects/cellpermission-element-assl.md), [cubo](../objects/cube-element-assl.md), [CubeDimensionPermission](../data-type/permission-data-type-assl.md), [base de datos](../objects/database-element-assl.md) , [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [dimensión](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [jerarquía](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [nivel](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [medida](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [ Partición](../objects/partition-element-assl.md), [permiso](../data-type/permission-data-type-assl.md), [perspectiva](../objects/perspective-element-assl.md), [rol](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [ Seguimiento](../objects/trace-element-assl.md), [traducción](../objects/translation-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de un elemento `Description` tiene las restricciones siguientes:  
  
-   El valor no puede contener espacios delante ni detrás. Si se incluyen espacios iniciales o finales en el valor de un `Description` elemento, esos espacios quitará implícitamente por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   El valor no puede contener caracteres de control. Si se incluyen caracteres de control en el valor de un elemento `Description`, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los quitará implícitamente.  
  
## <a name="see-also"></a>Vea también  
 [Nombre de elemento &#40;ASSL&#41;](name-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
