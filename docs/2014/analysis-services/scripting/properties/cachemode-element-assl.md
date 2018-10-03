---
title: Elemento CacheMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CacheMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- CacheMode element
ms.assetid: bfb8f7bb-ccd3-4dfe-a36a-1cea15edfe40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8c2011cf33695f9fa4933e63a8ad0c1685d7df01
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080295"
---
# <a name="cachemode-element-assl"></a>Elemento CacheMode (ASSL)
  Determina el mecanismo de almacenamiento en caché utilizado para los datos de aprendizaje recuperados al procesar una estructura de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructure>  
   ...  
   <CacheMode>...</CacheMode>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*KeepTrainingCases*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*KeepTrainingCases*|Los casos de aprendizaje se almacenan en memoria caché durante el procesamiento y después.|  
|*ClearAfterProcessing*|Los casos de aprendizaje se almacenan en memoria caché durante el procesamiento, perlo después se eliminan.|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `CacheMode` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
