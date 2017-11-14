---
title: Tipo de datos TableMiningStructureColumn (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- TableMiningStructureColumn Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TableMiningStructureColumn
helpviewer_keywords:
- TableMiningStructureColumn data type
ms.assetid: 350358b0-f2fc-43c3-957d-884c59fa879e
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7ba1195b1920625f8602a24f6ba8fa5879639fc5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="tableminingstructurecolumn-data-type-assl"></a>Tipo de datos TableMiningStructureColumn (ASSL)
  Define un tipo de datos derivado que representa un [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md) elemento que contiene tablas anidadas, a diferencia de los valores escalares asociados con la [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md) elemento contiene los valores escalares.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TableMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <ForeignKeyColumn>..</ForeignKeyColumn>  
   <SourceMeasureGroup>..</SourceMeasureGroup>  
   <Columns>..</Columns>  
   <Translations>..</Translations>  
</TableMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Columnas](../../../analysis-services/scripting/collections/columns-element-assl.md), [ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md), [SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md), [traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos derivados|[Columna](../../../analysis-services/scripting/objects/column-element-assl.md) ([columnas](../../../analysis-services/scripting/collections/columns-element-assl.md) colección de [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

