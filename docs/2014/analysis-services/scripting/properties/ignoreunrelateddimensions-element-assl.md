---
title: Elemento IgnoreUnrelatedDimensions (ASSL) | Microsoft Docs
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
- IgnoreUnrelatedDimensions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IgnoreUnrelatedDimensions
helpviewer_keywords:
- IgnoreUnrelatedDimensions element
ms.assetid: c7d7a1cd-a8e0-4ae7-9464-a1d2a55a86ab
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c278a3109180dbd058bc7ed8212c7b05782ce3d5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37295467"
---
# <a name="ignoreunrelateddimensions-element-assl"></a>Elemento IgnoreUnrelatedDimensions (ASSL)
  Determina si las dimensiones no relacionadas están forzadas a su nivel superior cuando los miembros de las dimensiones que no están relacionadas con el grupo de medida se incluyen en una consulta.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroup>  
   ...  
   <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|True|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MeasureGroup](../objects/group-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Si `IgnoreUnrelatedDimensions` es `true`, las dimensiones no relacionadas se fuerzan a su nivel superior; cuando el valor es `false`, las dimensiones no se fuerzan a su nivel superior. Esta propiedad es similar a expresiones multidimensionales (MDX) [ValidMeasure](/sql/mdx/validmeasure-mdx) función.  
  
 El elemento que se corresponde con el elemento primario de `IgnoreUnrelatedDimensions` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
