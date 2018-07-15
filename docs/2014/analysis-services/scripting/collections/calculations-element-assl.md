---
title: Elemento calculations (ASSL) | Microsoft Docs
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
- Calculations Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Calculations
helpviewer_keywords:
- Calculations element
ms.assetid: 03e5e91c-1f66-4dc7-8aad-4d9876928df0
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 130288eb3a628a746d3b7b19b1635a31250cdb8d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319295"
---
# <a name="calculations-element-assl"></a>Elemento Calculations (ASSL)
  Contiene la colección de [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elementos asociados con un [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Perspective>  
      ...  
   <Calculations>  
      <Calculation xsi:type="PerspectiveCalculation">...</Calculation>  
   </Calculations>  
   ...  
</Perspective>  
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
|Elementos primarios|[Perspectiva](../objects/perspective-element-assl.md)|  
|Elementos secundarios|[Cálculo](../objects/calculation-element-assl.md) typu [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.PerspectiveCalculationCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
