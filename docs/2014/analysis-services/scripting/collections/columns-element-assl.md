---
title: Elemento Columns (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Columns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- COLUMNS
helpviewer_keywords:
- Columns element
ms.assetid: 14011eed-6f10-4120-b256-d599d59bde80
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16e8d446b3ffeb4895bde76a739d7ec63a01337d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131515"
---
# <a name="columns-element-assl"></a>Elemento Columns (ASSL)
  Contiene la colección de columnas asociada al elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action xsi:type="DrillThroughAction"> <!-- or one of the elements listed below in the Element Relationships table -->  
   <Columns>  
      <Column xsi:type="MeasureBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="CubeAttributeBinding">...</Column> <!-- parent: DrillThroughAction -->  
      <!-- or -->  
      <Column xsi:type="EventColumn">...</Column> <!-- parent: Event -->  
      <!-- or -->  
      <Column xsi:type="MiningModelColumn">...</Column> <!-- parent: MiningModel or MiningModelColumn -->  
      <!-- or -->  
      <Column xsi:type="MiningStructureColumn">...</Column> <!-- parent: MiningStructure or TableMiningStructureColumn -->  
   </Columns>  
</DrillThroughAction>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[Evento](../objects/event-element-assl.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|Todos las demás|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acción](../objects/action-element-assl.md) typu [DrillThroughAction](../data-type/action-data-type-assl.md), [eventos](../objects/event-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md), [ MiningStructure](../objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[DrillThroughAction](../data-type/binding-data-type-assl.md) o [MeasureBinding](../data-type/measurebinding-data-type-assl.md)|  
|[Evento](../data-type/eventcolumn-data-type-assl.md)|  
|[MiningModel](../objects/miningmodel-element-assl.md), [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md), [TableMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para `DrillThroughAction` elementos, el `Columns` colección identifica las columnas que contienen datos que se devolverán cuando se realiza la acción.  
  
 Para `TableMiningStructureColumn` elementos, el `Columns` colección permite sólo un nivel de recursividad. En otras palabras, cualquier `TableMiningStructureColumn` los elementos incluidos en esta colección no pueden contener ninguno `TableMiningStructureColumn` elementos en su `Columns` colección.  
  
 Algunos de los elementos correspondientes en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.TraceColumnCollection>, <xref:Microsoft.AnalysisServices.MiningModelColumnCollection> y <xref:Microsoft.AnalysisServices.MiningStructureColumnCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
