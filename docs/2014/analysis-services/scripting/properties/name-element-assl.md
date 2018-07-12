---
title: Nombre de elemento (ASSL) | Microsoft Docs
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
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Name
helpviewer_keywords:
- Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7dde1de33d7ff2219bf2f73696c8a83236b46eb6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211595"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena (hasta 100 caracteres)|  
|Valor predeterminado|Varía|  
|Cardinalidad|1-1: elemento necesario que se produce solo una vez|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acción](../objects/action-element-assl.md), [agregación](../objects/aggregation-element-assl.md), [AggregationDesign](../objects/aggregationdesign-element-assl.md), [AlgorithmParameter](../objects/algorithmparameter-element-assl.md), [anotación](../objects/annotation-element-assl.md), [ Ensamblado](../objects/assembly-element-assl.md), [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md), [cubo](../objects/cube-element-assl.md), [CubeDimension](../data-type/dimension-data-type-assl.md), [CubeHierarchy](../data-type/hierarchy-data-type-assl.md), [Base de datos](../objects/database-element-assl.md), [DataSource](../objects/datasource-element-assl.md), [DataSourceView](../objects/datasourceview-element-assl.md), [dimensión](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [Grupo](../objects/group-element-assl.md), [jerarquía](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [nivel](../objects/level-element-assl.md), [MdxScript](../objects/mdxscript-element-assl.md), [ Medida](../objects/measure-element-assl.md), [MeasureGroup](../objects/measuregroup-element-assl.md), [MemberProperty](../objects/attributerelationship-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../objects/miningstructure-element-assl.md), [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md), [partición](../objects/partition-element-assl.md), [permiso](../data-type/permission-data-type-assl.md), [ Perspectiva](../objects/perspective-element-assl.md), [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md), [ReportFormatParameter](../objects/reportformatparameter-element-asl.md), [ReportParameter](../objects/reportparameter-element-assl.md), [ Rol](../objects/role-element-assl.md), [Server](../objects/server-element-assl.md), [ServerProperty](../objects/serverproperty-element-assl.md), [seguimiento](../objects/trace-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Todos los elementos que se usan para definir un objeto (una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], una jerarquía, un atributo etc.) tiene un `Name` elemento como una propiedad. El valor de un elemento `Name` tiene las restricciones siguientes:  
  
-   El valor no puede contener espacios delante ni detrás. Si se incluyen espacios al principio o al final del valor de un elemento `Name`, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] los quitará implícitamente.  
  
-   El valor no debe contener caracteres de control. Se desaconseja la presencia de caracteres de control en un nombre, ya que a veces puede producir errores de validación XML.  
  
     Para los objetos creados mediante el método `GetNewName` en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], AMO comprueba y posteriormente quita todos los caracteres de control, espacios iniciales o espacios finales del nombre. Por esta razón, el método recomendado para establecer nombres de objeto es mediante `GetNewName`.  
  
     Sin embargo, si establece la propiedad `Name` directamente, no se realizan las mismas comprobaciones de validación, pudiendo dar lugar a errores de validación XML. El hecho de que se produzca un error realmente depende del carácter de control que aparece en el nombre.  
  
     Aunque los caracteres de control nunca se deben usar en un nombre de objeto, Analysis Services no los impide expresamente. Las versiones anteriores de Analysis Services aceptaban algunas veces caracteres de control en un nombre de objeto. Por esta razón, [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] omitirá los caracteres de control en un nombre de objeto para evitar que las soluciones anteriores dejen de funcionar.  
  
-   No se pueden utilizar los valores reservados siguientes:  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   De COM1 a COM9 (COM1, COM2, COM3, etc.)  
  
    -   CON  
  
    -   De LPT1 a LPT9 (LPT1, LPT2, LPT3, etc.)  
  
    -   NUL  
  
    -   PRN  
  
 En la tabla siguiente se enumeran los caracteres adicionales que no se pueden utilizar dentro del valor de un elemento `Name`, en función del elemento primario.  
  
|Elemento primario|Caracteres no válidos|  
|--------------------|------------------------|  
|[Server](../objects/server-element-assl.md)|El nombre debe seguir las reglas de los nombres de equipo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Las direcciones IP no son válidas.|  
|[Origen de datos](../objects/datasource-element-assl.md)|:/\\*&#124;?" [] (){}<>|  
|[Nivel](../objects/level-element-assl.md), [atributo elemento](../objects/attribute-element-assl.md)|.,;' `:/\\*&#124;?" & % $! [] +={}<>|  
|Todos los demás elementos primarios|.,;' `:/\\*&#124;?" & % $! [] de () +={}<>|  
  
## <a name="see-also"></a>Vea también  
 [Id. de elemento &#40;ASSL&#41;](id-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
