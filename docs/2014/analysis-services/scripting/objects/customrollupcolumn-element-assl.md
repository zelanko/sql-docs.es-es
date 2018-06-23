---
title: Elemento CustomRollupColumn (ASSL) | Documentos de Microsoft
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
- CustomRollupColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CustomRollupColumn
helpviewer_keywords:
- CustomRollupColumn element
ms.assetid: 8c825f16-0d17-4ff8-bc18-b52cf11edba7
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e57329b1112441ddba51eeaaf709f18219d8db33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105949"
---
# <a name="customrollupcolumn-element-assl"></a>Elemento CustomRollupColumn (ASSL)
  Define los detalles de la columna que proporciona una fórmula de resumen personalizada.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <CustomRollupColumn xsi:type="DataItem">...</CustomRollupColumn>  
   ...  
</DimensionAttribute>  
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
|Elementos primarios|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para obtener información adicional acerca de la `DataItem` tipo, incluida una tabla de objetos de Analysis Services Scripting Language (ASSL) y las propiedades de la `DataItem` los tipos, vea [tipo de datos DataItem &#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md).  
  
 El elemento que corresponde al elemento primario de `CustomRollupColumn` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  