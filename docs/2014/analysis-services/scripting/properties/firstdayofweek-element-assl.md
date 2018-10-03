---
title: Elemento FirstDayOfWeek (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- FirstDayOfWeek Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FirstDayOfWeek
helpviewer_keywords:
- FirstDayOfWeek element
ms.assetid: d3c92fa3-b293-43b5-806e-cd1c146a3a7c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f1d3901e8e7205a2fcba7ab2967cc11b37abdcf6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168211"
---
# <a name="firstdayofweek-element-assl"></a>Elemento FirstDayOfWeek (ASSL)
  Define el primer día de la semana para un [TimeBinding](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TimeBinding>  
   ...  
   <FirstDayOfWeek>...</FirstDayOfWeek>  
   ...  
</TimeBinding>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Entero (entre 1 y 7, donde 1 = domingo y 7 = sábado)|  
|Valor predeterminado|`1`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[TimeBinding](../data-type/binding-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `FirstDayOfWeek` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
