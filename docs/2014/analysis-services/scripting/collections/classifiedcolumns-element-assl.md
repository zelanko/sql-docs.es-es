---
title: Elemento ClassifiedColumns (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClassifiedColumns Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClassifiedColumns
helpviewer_keywords:
- ClassifiedColumns element
ms.assetid: f16b4f51-c38d-4601-98b8-1497dbf12d02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e2624c2d944af873fe6a34cbd9ca3684050bf92
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209835"
---
# <a name="classifiedcolumns-element-assl"></a>Elemento ClassifiedColumns (ASSL)
  Contiene la colección de columnas relacionadas clasificadas por el [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructureColumn xsi:type="ScalarMiningStructureColumn">  
   ...  
   <ClassifiedColumns>  
      <ClassifiedColumnID>...</ClassifiedColumnID>  
   </ClassifiedColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) typu[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|[ClassifiedColumnID](../properties/id-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `ClassifiedColumns` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos MiningStructureColumn &#40;ASSL&#41;](../data-type/miningstructurecolumn-data-type-assl.md)   
 [Elemento MiningStructure &#40;ASSL&#41;](../objects/miningstructure-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
