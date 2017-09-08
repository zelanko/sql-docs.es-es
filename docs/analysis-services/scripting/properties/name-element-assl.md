---
title: Nombre de elemento (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Name Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Name
helpviewer_keywords:
- Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 10567ba5543e2ce231a0f690287e7fc19462ed87
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="name-element-assl"></a>Elemento Name (ASSL)
  Contiene el nombre del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena (hasta 100 caracteres)|  
|Valor predeterminado|Varía|  
|Cardinalidad|1-1: elemento necesario que se produce una vez y solo una vez|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md), [agregación](../../../analysis-services/scripting/objects/aggregation-element-assl.md), [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md), [anotación](../../../analysis-services/scripting/objects/annotation-element-assl.md), [ Ensamblado](../../../analysis-services/scripting/objects/assembly-element-assl.md), [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [Base de datos](../../../analysis-services/scripting/objects/database-element-assl.md), [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md), [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md), [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [Grupo](../../../analysis-services/scripting/objects/group-element-assl.md), [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [nivel](../../../analysis-services/scripting/objects/level-element-assl.md), [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md), [ Medida](../../../analysis-services/scripting/objects/measure-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md), [partición](../../../analysis-services/scripting/objects/partition-element-assl.md), [permiso](../../../analysis-services/scripting/data-type/permission-data-type-assl.md), [ Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md), [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md), [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md), [ Rol](../../../analysis-services/scripting/objects/role-element-assl.md), [Server](../../../analysis-services/scripting/objects/server-element-assl.md), [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md), [seguimiento](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Todos los elementos que se utilizan para definir un objeto (una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], una jerarquía, un atributo etc.) tiene un **nombre** elemento como una propiedad. El valor de un **nombre** elemento tiene las siguientes restricciones:  
  
-   El valor no puede contener espacios delante ni detrás. Si se incluyen espacios iniciales o finales en el valor de un **nombre** elemento, dichos espacios quitará implícitamente por [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
-   El valor no debe contener caracteres de control. Se desaconseja la presencia de caracteres de control en un nombre, ya que a veces puede producir errores de validación XML.  
  
     Para los objetos creados mediante el **GetNewName** método [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], AMO comprueba y posteriormente quita los caracteres de control, espacios, espacios iniciales o finales en el nombre. Para este motivo, con **GetNewName** es el enfoque recomendado para establecer los nombres de objeto.  
  
     Sin embargo, si establece la **nombre** propiedad directamente, la misma validación no se realizan comprobaciones, lo cual puede provocar errores de validación XML. El hecho de que se produzca un error realmente depende del carácter de control que aparece en el nombre.  
  
     Aunque los caracteres de control nunca se deben usar en un nombre de objeto, Analysis Services no los impide expresamente. Las versiones anteriores de Analysis Services aceptaban algunas veces caracteres de control en un nombre de objeto. Para este motivo, SQL Server 2016 Analysis Services y más adelante pasará por alto los caracteres de control en un nombre de objeto para evitar interrumpir las soluciones anteriores.  
  
-   No se pueden utilizar los valores reservados siguientes:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   De COM1 a COM9 (COM1, COM2, COM3, etc.)  
  
    -   CON  
  
    -   De LPT1 a LPT9 (LPT1, LPT2, LPT3, etc.)  
  
    -   NUL  
  
    -   PRN  
  
 En la tabla siguiente se enumera los caracteres adicionales que no se puede utilizar dentro del valor de un **nombre** elemento, en función del elemento primario.  
  
|Elemento primario|Caracteres no válidos|  
|--------------------|------------------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|El nombre debe seguir las reglas de los nombres de equipo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Las direcciones IP no son válidas.|  
|[Origen de datos](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"()[]{}<>|  
|[Nivel de](../../../analysis-services/scripting/objects/level-element-assl.md), [atributo elemento](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"&%$!+=[]{}<>|  
|Todos los demás elementos primarios|.,;'`:/\\*&#124;?"&%$!+=()[]{}<>|  
  
## <a name="see-also"></a>Vea también  
 [Id. de elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
