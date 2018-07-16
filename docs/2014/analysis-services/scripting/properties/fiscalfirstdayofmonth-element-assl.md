---
title: Elemento FiscalFirstDayOfMonth (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- FiscalFirstDayOfMonth Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FiscalFirstDayOfMonth
helpviewer_keywords:
- FiscalFirstDayOfMonth element
ms.assetid: f793e93f-62de-4c3b-90b0-a46bd3cadae5
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d183e519ddd3a103cd8e9cf90105b9c8848acb55
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235545"
---
# <a name="fiscalfirstdayofmonth-element-assl"></a>Elemento FiscalFirstDayOfMonth (ASSL)
  Define el primer día del mes fiscal para un [TimeBinding](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TimeBinding>  
   ...  
   <FiscalFirstDayOfMonth>...</FiscalFirstDayOfMonth>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Integer (entre 1 y 31)|  
|Valor predeterminado|`1`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que se corresponde con el elemento primario de `FiscalFirstDayOfMonth` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
