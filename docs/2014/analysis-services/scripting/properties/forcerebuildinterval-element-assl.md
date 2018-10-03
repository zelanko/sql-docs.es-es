---
title: Elemento ForceRebuildInterval (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ForceRebuildInterval Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ForceRebuildInterval
helpviewer_keywords:
- ForceRebuildInterval element
ms.assetid: d068f92e-4213-471c-a3a4-aec5af4b8ebf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7e888f045ae2305133c20375915936d4bce6695
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133634"
---
# <a name="forcerebuildinterval-element-assl"></a>Elemento ForceRebuildInterval (ASSL)
  Determina la cantidad de tiempo, a partir del momento en que una nueva imagen OLAP multidimensional (MOLAP) queda disponible, tras el que la creación de imágenes MOLAP se inicia incondicionalmente.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <ForceRebuildInterval>...</ForceRebuildInterval>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|XML duration|  
|Valor predeterminado|Infinite|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `ForceRebuildInterval` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
