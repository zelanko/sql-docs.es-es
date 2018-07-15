---
title: Elemento Annotation (ASSL) | Microsoft Docs
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
- Annotation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0453688aab37831c54bad3080a34409b078740bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304505"
---
# <a name="annotation-element-assl"></a>Elemento Annotation (ASSL)
  Contiene elementos que se utilizan para extender el esquema del lenguaje de scripting de Analysis Services (ASSL).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Anotaciones](../collections/annotations-element-assl.md)|  
|Elementos secundarios|[Nombre](../properties/name-element-assl.md), [valor](../properties/value-element-assl.md), [visibilidad](../properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento `Annotation` proporciona extensibilidad del esquema ASSL para todos los objetos distintos de los utilizados únicamente para definir un tipo de datos complejo. El elemento `Value` del elemento `Annotation` puede contener XML válido de cualquier espacio de nombres XML distinto de ASSL, sujeto a las reglas siguientes:  
  
-   El XML solo puede contener elementos.  
  
-   Cada elemento debe tener un nombre único. Se recomienda que el valor del elemento `Name` del elemento `Annotation` haga referencia al espacio de nombres de destino.  
  
 Estas reglas se imponen para permitir que el contenido del elemento `Annotation` se exponga como un conjunto de pares de nombre/valor a través de otras interfaces, como Objetos de ayuda para la toma de decisiones (DSO).  
  
 No se pueden conservar los comentarios y los espacios en blanco dentro del elemento `Annotation` que no se incluyen dentro de un elemento secundario. Además, todos los elementos deben ser de lectura y escritura; se omitirán los elementos de solo lectura.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Annotation>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
