---
title: Elemento Annotation (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 303ed41b27538d5e21541e2912e892d91fd0f3d0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034484"
---
# <a name="annotation-element-assl"></a>Elemento Annotation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|Elementos secundarios|[Nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [valor](../../../analysis-services/scripting/properties/value-element-assl.md), [visibilidad](../../../analysis-services/scripting/properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **anotación** elemento proporciona extensibilidad del esquema ASSL para todos los objetos que no sean los que se usan únicamente para definir un tipo de datos complejos. El **valor** elemento de la **anotación** elemento puede contener XML válido de cualquier espacio de nombres XML distinto de ASSL, sujeto a las reglas siguientes:  
  
-   El XML solo puede contener elementos.  
  
-   Cada elemento debe tener un nombre único. Se recomienda que el valor de la **nombre** elemento de la **anotación** elemento hacer referencia el espacio de nombres de destino.  
  
 Estas reglas se imponen para permitir que el contenido de la **anotación** pares de elemento que se va a exponer como un conjunto de nombre/valor mediante otras interfaces, como Decision Support Objects (DSO).  
  
 Comentarios y espacios en blanco dentro del **anotación** no se puede conservar el elemento que no se incluyen dentro de un elemento secundario. Además, todos los elementos deben ser de lectura y escritura; se omitirán los elementos de solo lectura.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Annotation>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
