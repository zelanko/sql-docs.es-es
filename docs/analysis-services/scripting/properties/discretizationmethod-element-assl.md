---
title: Elemento DiscretizationMethod (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DiscretizationMethod Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DiscretizationMethod
helpviewer_keywords:
- DiscretizationMethod element
ms.assetid: 4cfe015f-ad6c-47e1-8aff-c9c7677867b1
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d6ba31aa8494dc918ba69118a025dc9ae32bcaaa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="discretizationmethod-element-assl"></a>Elemento DiscretizationMethod (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define el método que se va a utilizar para la discretización.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationMethod>...</DiscretizationMethod>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*None*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor del elemento **DiscretizationMethod** determina cómo se crean u organizan muchos grupos o depósitos cuando se discretizan los valores de **DimensionAttribute** o **ScalarMiningStructureColumn** en conjuntos de grupos específicos. Para obtener más información acerca de los métodos de discretización, vea [métodos de discretización &#40;minería de datos&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Automática*|Equivale al método de discretización AUTOMATIC para las columnas de estructura de minería de datos.|  
|*EqualAreas*|Equivale al método de discretización EQUAL_AREAS para las columnas de estructura de minería de datos.|  
|*Clusters*|Equivale al método de discretización CLUSTERS para las columnas de estructura de minería de datos.|  
|*Umbrales*|Equivale al método de discretización THRESHOLDS para las columnas de estructura de minería de datos.|  
|*EqualRanges*|Equivale al método de discretización EQUAL_RANGES para las columnas de estructura de minería de datos.|  
  
 La enumeración que corresponde a los valores permitidos para **DiscretizationMethod** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
