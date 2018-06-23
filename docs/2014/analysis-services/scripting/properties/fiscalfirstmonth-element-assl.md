---
title: Elemento FiscalFirstMonth (ASSL) | Documentos de Microsoft
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
- FiscalFirstMonth Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FiscalFirstMonth
helpviewer_keywords:
- FiscalFirstMonth element
ms.assetid: 30766baa-ebec-4425-93de-7defe4d6e571
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1c7a1b39a6950791a0e38fa1e43b69ce11214c8e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103168"
---
# <a name="fiscalfirstmonth-element-assl"></a>Elemento FiscalFirstMonth (ASSL)
  Define el primer mes del período fiscal para un [TimeBinding](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TimeBinding>  
   ...  
   <FiscalFirstMonth>...</FiscalFirstMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Entero (de 1 a 12, donde 1 = enero y 12 = diciembre)|  
|Valor predeterminado|`1`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que corresponde al elemento primario de `FiscalFirstMonth` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  