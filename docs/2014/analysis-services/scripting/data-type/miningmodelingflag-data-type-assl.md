---
title: Tipo de datos MiningModelingFlag (ASSL) | Microsoft Docs
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
- MiningModelingFlag Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelingFlag
helpviewer_keywords:
- MiningModelingFlag data type
ms.assetid: aaa72ba8-051e-4b01-b1e9-9c8d83b8b752
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ece92d63c0d66c1ef845ce2d28d3317b2f65d66f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167526"
---
# <a name="miningmodelingflag-data-type-assl"></a>Tipo de datos MiningModelingFlag (ASSL)
  Define un tipo de datos primitivo que representa las marcas de modelado disponibles para un [ModelingFlag](../objects/modelingflag-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModelingFlag>...</MiningModelingFlag>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|String (enumeración)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|None|  
|Elementos derivados|[ModelingFlag](../objects/modelingflag-element-assl.md) ([ModelingFlags](../collections/modelingflags-element-assl.md) colección de [MiningModelColumn](miningmodelcolumn-data-type-assl.md) o [ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El nombre de la marca puede contener espacios. Los valores que se admiten de forma nativa son los de la lista siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*MODEL_EXISTENCE_ONLY*|La columna se debe modelar con dos estados, ausente y presente, sin tener en cuenta los valores de la columna. Esto es particularmente útil para las columnas de una tabla anidada, donde los valores están dispersos por los casos.|  
|*NO ES NULL*|La columna no puede aceptar valores NULL.|  
|*REGRESSOR*|La columna proporciona valores de regresor para los casos de prueba.|  
  
 Otras marcas específicas del proveedor pueden usarse si se han agregado proveedores de minería de datos de OLE DB o datos de otros fabricantes en la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Un elemento estrechamente relacionado del modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.MiningModelingFlags>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
