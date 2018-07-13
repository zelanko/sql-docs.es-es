---
title: Elemento ID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c323bd71865d0dd09bf724373ece03d83e7608ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209945"
---
# <a name="id-element-assl"></a>Elemento ID (ASSL)
  Contiene el identificador único (id.) del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action> <!-- or one of the elements listed in the Element Relationships table -->  
   ...  
   <ID>...</ID>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena (hasta 100 caracteres)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acción](../objects/action-element-assl.md), [agregación](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [ensamblado](../objects/assembly-element-assl.md), [cubo](../objects/cube-element-assl.md), [CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [base de datos](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [dimensión ](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [jerarquía](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [nivel](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [Medida](../objects/measure-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MeasureGroupBinding](../data-type/binding-data-type-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [ MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [partición](../objects/partition-element-assl.md), [permiso](../data-type/permission-data-type-assl.md), [Perspectiva](../objects/perspective-element-assl.md), [rol](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [seguimiento](../objects/trace-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Todos los objetos principales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tiene un `ID` elemento como una propiedad. El valor de un `ID` elemento tiene las siguientes restricciones:  
  
-   El valor no puede contener espacios delante ni detrás. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quitará implícitamente los espacios delante o detrás del valor de un elemento `ID`.  
  
-   El valor no puede contener caracteres de control. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] quitará implícitamente los caracteres de control del valor de un elemento `ID`.  
  
-   No se pueden utilizar los valores reservados siguientes:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   De COM1 a COM9 (COM1, COM2, COM3, etc.)  
  
    -   CON  
  
    -   De LPT1 a LPT9 (LPT1, LPT2, LPT3, etc.)  
  
    -   NUL  
  
    -   PRN  
  
 En la tabla siguiente se enumera los caracteres adicionales que no se puede usar dentro del valor de un `ID` elemento, en función del elemento primario.  
  
|Elemento primario|Characters|  
|--------------------|----------------|  
|[Server](../objects/server-element-assl.md)|El valor debe seguir las reglas de los nombres de equipo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. (Las direcciones IP no son válidas.)|  
|[Origen de datos](../objects/datasource-element-assl.md)|:/\\*&#124;?" [] (){}<>|  
|[Nivel](../objects/level-element-assl.md), [atributo elemento](../objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! [] +={}<>|  
|Todos los demás elementos primarios|.,;' `:/\\*&#124;?" & % $! [] de () +={}<>|  
  
## <a name="see-also"></a>Vea también  
 [Nombre de elemento &#40;ASSL&#41;](name-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
