---
title: Elemento ReportingFirstMonth (ASSL) | Microsoft Docs
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
- ReportingFirstMonth Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportingFirstMonth
helpviewer_keywords:
- ReportingFirstMonth element
ms.assetid: cdce83ab-ac22-4f4a-b8f2-1739883be8dd
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 702d7e17e35e334e982ba3a230af5b1506f3d071
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275221"
---
# <a name="reportingfirstmonth-element-assl"></a>Elemento ReportingFirstMonth (ASSL)
  Define el primer mes de informes para la [TimeBinding](../data-type/binding-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TimeBinding>  
   ...  
   <ReportingFirstMonth>...</ReportingFirstMonth>  
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
 El elemento que se corresponde con el elemento primario de `ReportingFirstMonth` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.TimeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
