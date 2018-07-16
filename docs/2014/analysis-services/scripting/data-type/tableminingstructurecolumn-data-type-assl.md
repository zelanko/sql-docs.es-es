---
title: Tipo de datos TableMiningStructureColumn (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableMiningStructureColumn
helpviewer_keywords:
- TableMiningStructureColumn data type
ms.assetid: 350358b0-f2fc-43c3-957d-884c59fa879e
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2e03fec81f796ccf87f19df9b2e43fe29b0e318e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319405"
---
# <a name="tableminingstructurecolumn-data-type-assl"></a>Tipo de datos TableMiningStructureColumn (ASSL)
  Define un tipo de datos derivado que representa un [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) elemento que contiene tablas anidadas, a diferencia de los valores escalares asociados con el [ScalarMiningStructureColumn](scalarminingstructurecolumn-data-type-assl.md) elemento que contiene valores escalares.  
  
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
|Tipos de datos base|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Columnas](../collections/columns-element-assl.md), [ForeignKeyColumn](../objects/column-element-assl.md), [SourceMeasureGroup](../objects/group-element-assl.md), [traducciones](../collections/translations-element-assl.md)|  
|Elementos derivados|[Columna](../objects/column-element-assl.md) ([columnas](../collections/columns-element-assl.md) colección de [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TableMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
