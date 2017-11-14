---
title: Id. de elemento (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ID
helpviewer_keywords:
- ID element
ms.assetid: ea3ce0f4-9084-45d0-8150-73afb7005af2
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e18410dd661afc19e42ba735f30728cad8f49bfc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena (hasta 100 caracteres)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md), [agregación](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [ensamblado](../../../analysis-services/scripting/objects/assembly-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [dimensión ](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [nivel](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [Medida](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [ MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [partición](../../../analysis-services/scripting/objects/partition-element-assl.md), [permiso](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md), [rol](../../../analysis-services/scripting/objects/role-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md), [seguimiento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Todos los objetos principales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tiene un **identificador** elemento como una propiedad. El valor de un **identificador** elemento tiene las siguientes restricciones:  
  
-   El valor no puede contener espacios delante ni detrás. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]quitará implícitamente los espacios iniciales o finales del valor de un **identificador** elemento.  
  
-   El valor no puede contener caracteres de control. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]quitará implícitamente los caracteres de control del valor de un **identificador** elemento.  
  
-   No se pueden utilizar los valores reservados siguientes:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   De COM1 a COM9 (COM1, COM2, COM3, etc.)  
  
    -   CON  
  
    -   De LPT1 a LPT9 (LPT1, LPT2, LPT3, etc.)  
  
    -   NUL  
  
    -   PRN  
  
 En la tabla siguiente se enumera los caracteres adicionales que no se puede utilizar dentro del valor de un **identificador** elemento, en función del elemento primario.  
  
|Elemento primario|Characters|  
|--------------------|----------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|El valor debe seguir las reglas de los nombres de equipo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. (Las direcciones IP no son válidas.)|  
|[Origen de datos](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[Nivel de](../../../analysis-services/scripting/objects/level-element-assl.md), [atributo elemento](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|Todos los demás elementos primarios|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>Vea también  
 [Name, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

