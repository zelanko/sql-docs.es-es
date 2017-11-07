---
title: Elemento Algorithm (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Algorithm Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fe1a9caffdff1de0dc62c4ddd696e1ec8b829bd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="algorithm-element-assl"></a>Elemento Algorithm (ASSL)
  Define el algoritmo usado por un [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **algoritmo** elemento es una cadena que identifica el algoritmo. Por ejemplo, podría ser la cadena *Microsoft_Naive_Bayes*, *Microsoft_Decision_Trees*, o *Microsoft_Clustering.* La cadena identifica los algoritmos proporcionados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y algoritmos personalizados proporcionados por el usuario. Los valores disponibles para la **algoritmo** se puede recuperar el elemento de la columna SERVICE_NAME de la [DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md) de filas de esquema.  
  
 El elemento que corresponde al elemento primario de **algoritmo** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningModel>. Un elemento estrechamente relacionado en el modelo de objetos de Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>.  
  
## <a name="see-also"></a>Vea también  
 [Algorithmparameter, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)   
 [AlgorithmParameters, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

