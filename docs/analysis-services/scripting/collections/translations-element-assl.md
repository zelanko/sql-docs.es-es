---
title: Elemento Translations (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
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
apiname: Translations Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Translations
helpviewer_keywords: Translations element
ms.assetid: 7f6b8ff2-e834-44d3-a176-216203158a8d
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4477a8b717a94465e7b56b03404e079ff9f6f4d9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="translations-element-assl"></a>Elemento Translations (ASSL)
  Contiene la colección de [traducción](../../../analysis-services/scripting/objects/translation-element-assl.md) elementos asociados con el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action><!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Translations>  
      <Translation>...</Translation>  
      <!-- or -->  
      <Translation xsi:type="AttributeTranslation">...</Translation><!-- parent: DimensionAttribute or ScalarMiningStructureColumn -->  
      <!-- or -->  
      <Translation xsi:type="RelationshipEndTranslation">...</Translation><!-- parent: RelationshipEnd -->  
   </Translations>  
   ...  
</Action>  
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
|Elementos primarios|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md), [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md), [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md), [Base de datos](../../../analysis-services/scripting/objects/database-element-assl.md), [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [Nivel](../../../analysis-services/scripting/objects/level-element-assl.md), [medida](../../../analysis-services/scripting/objects/measure-element-assl.md), [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md), [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md), [ Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md), [RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md), [TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|Vea la siguiente tabla.|  
  
|Antecesor o elemento primario|Elemento secundario|  
|------------------------|-------------------|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md) o [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[Traducción](../../../analysis-services/scripting/objects/translation-element-assl.md) de tipo [AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|  
|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|[Traducción](../../../analysis-services/scripting/data-type/relationshipendtranslation-element-assl.md) de tipo [RelationshipEndTranslation](../../../analysis-services/scripting/data-type/relationshipendtranslation-element-assl.md)|  
|Todos los demás|[Traducción](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.TranslationCollection> y <xref:Microsoft.AnalysisServices.AttributeTranslationCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
