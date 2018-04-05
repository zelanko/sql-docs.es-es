---
title: Elemento Annotation (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Annotation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 09cafc5c5dcbafd48047995b03082a4d15e84288
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="annotation-element-assl"></a>Elemento Annotation (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Contiene elementos que se usan para extender el esquema de Analysis Services Scripting Language (ASSL).  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
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
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
