---
title: Tipo de datos PerspectiveDimension (ASSL) | Documentos de Microsoft
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
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b2ec6ecb714ad87b32683f667514fe4badcabeda
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198749"
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
|Elementos secundarios|[Anotaciones](../collections/annotations-element-assl.md), [atributos](../collections/attributes-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md), [jerarquías](../collections/hierarchies-element-assl.md)|  
|Elementos derivados|[Dimensión](../objects/dimension-element-assl.md) ([dimensiones](../collections/dimensions-element-assl.md) colección de [perspectiva](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.PerspectiveDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  