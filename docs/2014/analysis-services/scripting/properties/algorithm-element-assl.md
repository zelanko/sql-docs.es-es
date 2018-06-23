---
title: Elemento Algorithm (ASSL) | Documentos de Microsoft
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
- Algorithm Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 86e44cf8069d9ed78a414cad5ac5079f8f2faa22
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200221"
---
# <a name="algorithm-element-assl"></a>Elemento Algorithm (ASSL)
  Define el algoritmo usado por un [MiningModel](../objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../objects/miningmodel-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor del elemento `Algorithm` es una cadena que identifica el algoritmo. Por ejemplo, podría ser la cadena *Microsoft_Naive_Bayes*, *Microsoft_Decision_Trees*, o *Microsoft_Clustering.* La cadena identifica los algoritmos proporcionados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y algoritmos personalizados proporcionados por el usuario. Los valores disponibles para la `Algorithm` se puede recuperar el elemento de la columna SERVICE_NAME de la [DMSCHEMA_MINING_SERVICES](../../schema-rowsets/data-mining/dmschema-mining-services-rowset.md) de filas de esquema.  
  
 El elemento que corresponde al elemento primario de `Algorithm` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningModel>. Un elemento estrechamente relacionado en el modelo de objetos de Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento AlgorithmParameter &#40;ASSL&#41;](../objects/algorithmparameter-element-assl.md)   
 [Elemento AlgorithmParameters &#40;ASSL&#41;](../collections/algorithmparameters-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  