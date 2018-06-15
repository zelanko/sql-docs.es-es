---
title: Códigos de tipo que se utilizan en los seguimientos de objeto de Analysis Services | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4d451b0348604c4b824bb5bf77c0e719990b1643
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34043949"
---
# <a name="analysis-services-object-type-codes-used-in-traces"></a>Códigos de tipo de objeto de Analysis Services usados en seguimientos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En esta página se indica el tipo de objeto (un número de seis dígitos) de cada objeto en un modelo de datos de Analysis Services.  Estos códigos aparecen en registros de seguimiento y se usan para identificar el tipo de objeto asociado con un bloqueo concreto. Por ejemplo, un tiempo de espera de bloqueo en una base de datos indicará el tipo de objeto 100002, que es el tipo de objeto Database.  
  
> [!NOTE]  
>  Aquí se enumeran más códigos de los que realmente aparecerán en un registro de seguimiento. La lista que aparece a continuación es una lista exhaustiva de los códigos de tipo para cada objeto, pero solo los objetos que llevan bloqueo presentarán un código de tipo de objeto en un registro de seguimiento.  
  
## <a name="object-type-reference"></a>Referencia de tipo de objeto  
  
|Tipo de objeto|Nombre del objeto|  
|-----------------|-----------------|  
|100000|Server|  
|100001|Comando|  
|100002|Base de datos|  
|100003|DataSource|  
|100004|DatabasePermission|  
|100005|Rol|  
|100006|Dimensión|  
|100007|DimensionAttribute|  
|100008|Jerarquía|  
|100009|Nivel|  
|100010|Cube|  
|100011|CubePermission|  
|100012|CubeDimension|  
|100013|CubeAttribute|  
|100014|CubeHierarchy|  
|100016|MeasureGroup|  
|100017|MeasureGroupDimension|  
|100018|MeasureGroupAttribute|  
|100020|Measure|  
|100021|Partición|  
|100025|AggregationDesign|  
|100026|AggregationDesignDimension|  
|100027|AggregationDesignAttribute|  
|100028|Agregación|  
|100029|AggregationDimension|  
|100030|AggregationAttribute|  
|100032|MiningStructure|  
|100033|MiningStructureColumn|  
|100037|MiningModel|  
|100038|MiningModelColumn|  
|100039|AlgorithmParameter|  
|100041|MiningModelPermission|  
|100042|DimensionPermission|  
|100043|MiningStructurePermission|  
|100044|Ensamblado|  
|100045|DatabaseRole|  
|100046|AttributePermission|  
|100047|CubeAttributePermission|  
|100048|CellPermission|  
|100049|CubeDimensionPermission|  
|100050|Seguimiento|  
|100051|ServerAssembly|  
|100052|CubeAssembly|  
|100053|Comando|  
|100054|KPI|  
|100055|DataSourceView|  
|100056|Perspective|  
|100100|CommandCollection|  
|100101|DatabaseCollection|  
|100102|DataSourceCollection|  
|100103|DatabasePermission|  
|100104|RoleCollection|  
|100105|DimensionCollection|  
|100106|DimensionAttributeCollection|  
|100107|HierarchyCollection|  
|100108|LevelCollection|  
|100109|CubeCollection|  
|100110|CubePermissionCollection|  
|100111|CubeDimensionCollection|  
|100112|CubeAttributeCollection|  
|100113|CubeHierarchyCollection|  
|100115|MeasureGroupCollection|  
|100116|MeasureGroupDimensionCollection|  
|100117|MeasureGroupAttributeCollection|  
|100119|MeasureCollection|  
|100120|PartitionCollection|  
|100124|AggregationDesignCollection|  
|100125|AggregationDesignDimensionCollection|  
|100126|AggregationDesignAttributeCollection|  
|100127|AggregationCollection|  
|100128|AggregationDimensionCollection|  
|100129|AggregationAttributeCollection|  
|100131|MiningStructureCollection|  
|100132|MiningStructureColumnCollection|  
|100136|MiningModelCollection|  
|100137|MiningModelColumnCollection|  
|100138|AlgorithmParameterCollection|  
|100140|MiningModelPermissionCollection|  
|100141|DimensionPermissionCollection|  
|100142|MiningStructurePermissionCollection|  
|100143|AssemblyCollection|  
|100144|DatabaseRoleCollecction|  
|100145|AttributePermissionCollection|  
|100146|CubeAttributePermissionCollection|  
|100147|CellPermissionCollection|  
|100148|CubeDimensionPermissionCollection|  
|100149|TraceCollection|  
|100150|ServerAssemblyCollection|  
|100151|CubeAssemblyCollection|  
|100152|CommandCollection|  
|100153|KpiCollection|  
|100154|DataSourceViewCollection|  
|100155|PerspectiveCollection|  
  
  
