---
title: Elemento ForeignKeyColumns (ASSL) | Documentos de Microsoft
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
- ForeignKeyColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForeignKeyColumns
helpviewer_keywords:
- ForeignKeyColumns element
ms.assetid: 0a673c1a-73dd-4217-aa41-56b340b5e1ab
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: da17077a4a75efc53de65b2168a5332db137bfd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113672"
---
# <a name="foreignkeycolumns-element-assl"></a>Elemento ForeignKeyColumns (ASSL)
  Contiene la colección de columnas que identifican la unión a la tabla primaria para un origen de datos relacional.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructureColumn xsi:type="TableMiningStructureColumn">  
   ...  
   <ForeignKeyColumns>  
      <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
...</ForeignKeyColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) de tipo [TableMiningStructureColumn](../data-type/tableminingstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|[ForeignKeyColumn](../objects/column-element-assl.md) de tipo [DataItem](../data-type/dataitem-data-type-assl.md)|  
  
## <a name="see-also"></a>Vea también  
 [Elemento MiningStructure &#40;ASSL&#41;](../objects/miningstructure-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  