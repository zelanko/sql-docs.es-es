---
title: Tipo de datos PerspectiveDimension (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PerspectiveDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveDimension
helpviewer_keywords:
- PerspectiveDimension data type
ms.assetid: c4bc56de-4f42-4ceb-a68d-a4fec92fdfa9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec49cb024ee678d83801812f8f8bd551fed48854
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196975"
---
# <a name="perspectivedimension-data-type-assl"></a>Tipo de datos PerspectiveDimension (ASSL)
  Define un tipo de datos primitivo que representa información sobre una dimensión en una perspectiva.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PerspectiveDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
   <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotations>  
</PerspectiveDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [atributos](../collections/attributes-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md), [jerarquías](../collections/hierarchies-element-assl.md)|  
|Elementos derivados|[Dimensión](../objects/dimension-element-assl.md) ([dimensiones](../collections/dimensions-element-assl.md) colección de [perspectiva](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.PerspectiveDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
