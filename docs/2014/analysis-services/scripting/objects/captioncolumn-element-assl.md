---
title: Elemento CaptionColumn (ASSL) | Documentos de Microsoft
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
- CaptionColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CaptionColumn
helpviewer_keywords:
- CaptionColumn element
ms.assetid: bdb1b9b8-b5d5-4d91-81c7-8de8635bbb83
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 58d10ce00adaa3593f50be99383bdfbdbee14441
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198536"
---
# <a name="captioncolumn-element-assl"></a>Elemento CaptionColumn (ASSL)
  Define la columna que proporciona el título para el atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeTranslation>  
   ...  
   <CaptionColumn xsi:type="DataItem">...</CaptionColumn>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Elemento de datos](../data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AttributeTranslation](../data-type/translation-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre la `DataItem` tipo, incluida una tabla de objetos de Analysis Services Scripting Language (ASSL) y las propiedades de la `DataItem` los tipos, vea [tipo de datos DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 El elemento que corresponde al elemento primario de `CaptionColumn` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.AttributeTranslation>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  