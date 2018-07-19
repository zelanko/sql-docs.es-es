---
title: Elemento DiscretizationMethod (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 81064689788574061f103b973a5435beb3e83893
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002207"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Ninguno*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor del elemento **DiscretizationMethod** determina cómo se crean u organizan muchos grupos o depósitos cuando se discretizan los valores de **DimensionAttribute** o **ScalarMiningStructureColumn** en conjuntos de grupos específicos. Para obtener más información acerca de los métodos de discretización, vea [métodos de discretización &#40;minería de datos&#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Automático*|Equivale al método de discretización AUTOMATIC para las columnas de estructura de minería de datos.|  
|*EqualAreas*|Equivale al método de discretización EQUAL_AREAS para las columnas de estructura de minería de datos.|  
|*Clústeres*|Equivale al método de discretización CLUSTERS para las columnas de estructura de minería de datos.|  
|*Umbrales*|Equivale al método de discretización THRESHOLDS para las columnas de estructura de minería de datos.|  
|*EqualRanges*|Equivale al método de discretización EQUAL_RANGES para las columnas de estructura de minería de datos.|  
  
 La enumeración que corresponde a los valores permitidos para **DiscretizationMethod** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DiscretizationMethod>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
