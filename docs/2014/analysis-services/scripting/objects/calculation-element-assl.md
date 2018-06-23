---
title: Elemento Calculation (ASSL) | Documentos de Microsoft
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
- Calculation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Calculation
helpviewer_keywords:
- Calculation element
ms.assetid: c96e37cf-b7ff-4296-a043-f9a5a5c444ce
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7368af0fa063e3c3372e594d1108173a614243d6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105256"
---
# <a name="calculation-element-assl"></a>Elemento Calculation (ASSL)
  Asocia un cálculo con un [perspectiva](perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Calculations>  
   <Calculation xsi:type="PerspectiveCalculation">  
      </Calculation>  
</Calculations>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cálculos](../collections/calculations-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.CalculationType> y <xref:Microsoft.AnalysisServices.PerspectiveCalculationType>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  