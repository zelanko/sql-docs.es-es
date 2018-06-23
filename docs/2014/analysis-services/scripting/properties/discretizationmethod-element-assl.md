---
title: Elemento DiscretizationMethod (ASSL) | Documentos de Microsoft
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
- DiscretizationMethod Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c22387c74c49446c74b06125da02bda11acd0b7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106429"
---
# <a name="discretizationmethod-element-assl"></a>Elemento DiscretizationMethod (ASSL)
  Define el método que se va a utilizar para la discretización.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Ninguno*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de la `DiscretizationMethod` elemento determina cómo los valores para la `DimensionAttribute` o `ScalarMiningStructureColumn` son discretizado o se organizan en un conjunto específico de grupos. Para obtener más información acerca de los métodos de discretización, vea [métodos de discretización &#40;minería de datos&#41;](../../data-mining/discretization-methods-data-mining.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Automático*|Equivale al método de discretización AUTOMATIC para las columnas de estructura de minería de datos.|  
|*EqualAreas*|Equivale al método de discretización EQUAL_AREAS para las columnas de estructura de minería de datos.|  
|*Clústeres*|Equivale al método de discretización CLUSTERS para las columnas de estructura de minería de datos.|  
|*Umbrales*|Equivale al método de discretización THRESHOLDS para las columnas de estructura de minería de datos.|  
|*EqualRanges*|Equivale al método de discretización EQUAL_RANGES para las columnas de estructura de minería de datos.|  
  
 La enumeración que corresponde a los valores permitidos de `DiscretizationMethod` en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  