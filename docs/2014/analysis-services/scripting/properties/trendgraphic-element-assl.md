---
title: Elemento TrendGraphic (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- TrendGraphic Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TrendGraphic
helpviewer_keywords:
- TrendGraphic element
ms.assetid: 7448fd80-3072-4d85-b3a0-6606d1d20885
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9766ee265450b31c7bbb062c9f632a2fb0be032
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102505"
---
# <a name="trendgraphic-element-assl"></a>Elemento TrendGraphic (ASSL)
  Contiene la representación gráfica recomendada de la tendencia de la [Kpi](../objects/kpi-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Kpi>  
   ...  
   <TrendGraphic>...</TrendGraphic>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[KPI](../objects/kpi-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Flecha estándar*|Flecha estándar|  
|*Flecha de estado - ascendente*|Flecha de estado|  
|*Flecha de estado: descendente*|Flecha de estado invertida|  
|*Cara sonriente*|Cara|  
  
 El elemento que se corresponde con el elemento primario de `TrendGraphic` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
