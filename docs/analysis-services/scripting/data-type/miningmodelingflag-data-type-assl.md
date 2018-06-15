---
title: Tipo de datos MiningModelingFlag (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffbf5b43efb72e32b49cf70a1a114a4b2c07b3de
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029362"
---
# <a name="miningmodelingflag-data-type-assl"></a>Tipo de datos MiningModelingFlag (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo que representa las marcas de modelado disponibles para un elemento [ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|String (enumeración)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|Ninguno|  
|Elementos derivados|[ModelingFlag](../../../analysis-services/scripting/objects/modelingflag-element-assl.md) (colección[ModelingFlags](../../../analysis-services/scripting/collections/modelingflags-element-assl.md) de [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md) o [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El nombre de la marca puede contener espacios. Los valores que se admiten de forma nativa son los de la lista siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|La columna se debe modelar con dos estados, ausente y presente, sin tener en cuenta los valores de la columna. Esto es particularmente útil para las columnas de una tabla anidada, donde los valores están dispersos por los casos.|  
|*NO ES NULL*|La columna no puede aceptar valores NULL.|  
|*REGRESSOR*|La columna proporciona valores de regresor para los casos de prueba.|  
  
 Se pueden utilizar otras marcas específicas del proveedor si se han agregado proveedores de OLE DB o de minería de datos de otros fabricantes a la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Un elemento estrechamente relacionado del modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.MiningModelingFlags>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
