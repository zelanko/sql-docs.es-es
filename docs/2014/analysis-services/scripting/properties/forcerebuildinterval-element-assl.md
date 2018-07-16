---
title: Elemento ForceRebuildInterval (ASSL) | Microsoft Docs
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
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa11e0fda75e55f5f8d9af5414203c7822cb5eb1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249055"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
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
  
## <a name="remarks"></a>Notas  
 El elemento que se corresponde con el elemento primario de `ForceRebuildInterval` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
