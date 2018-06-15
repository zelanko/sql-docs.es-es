---
title: Tipo de datos DegenerateMeasureGroupDimension (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e2e240f3f1131162dbde961da20dcfe9803213bc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029056"
---
# <a name="degeneratemeasuregroupdimension-data-type-assl"></a>Tipo de datos DegenerateMeasureGroupDimension (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos derivado que representa la relación entre una dimensión degenerada (es decir, una dimensión de hechos) y un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DegenerateMeasureGroupDimension>  
   <!-- DegenerateMeasureGroupDimension does not have any elements that extend RegularMeasureGroupDimension -->  
</DegenerateMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|Ninguno|  
|Elementos derivados|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de las dimensiones de hechos, vea [las relaciones entre dimensiones](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DegenerateMeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
