---
title: ValidMeasure (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- VALIDMEASURE
dev_langs:
- kbMDX
helpviewer_keywords:
- ValidMeasure function
ms.assetid: ecf20a86-c45e-4521-84ce-3a466e0c1136
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 343ebe6da0613d273dc16bd1b76826910179db2e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor de una medida de un cubo al forzar dimensiones no aplicables al nivel All (o el miembro predeterminado si no es agregable) cuando se devuelve el resultado de una tupla especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
## <a name="remarks"></a>Comentarios  
 El **ValidMeasure** función devuelve el valor de una tupla, omitiendo los atributos que no tienen relación con el grupo de medida de la medida cuyo valor devuelve la tupla. Un atributo puede no estar relacionado con una medida por dos razones:  
  
-   La dimensión del atributo no tiene ninguna relación con el grupo de medida de la medida de la tupla.  
  
-   La dimensión del atributo no tiene una relación con el grupo de medida de la medida, pero el atributo de granularidad no es el atributo clave y el atributo de granularidad no tiene una relación directa con el atributo en la tupla.  
  
 El comportamiento especificado por esta función es el comportamiento predeterminado del servidor y se controla mediante la **IgnoreUnrelatedDimensions** propiedad en el objeto de grupo de medida.  
  
 En cada atributo de la tupla especificada con granularidad (es decir, donde el miembro de la tupla no es el miembro All), la coordenada actual de cada uno de esos atributos se mueve de la siguiente manera:  
  
-   Los atributos relacionados con el miembro de atributo especificado se mueven al miembro que existe con el miembro actual.  
  
-   Los atributos que se relacionan con el miembro de atributo especificado se mueven al miembro All (o al miembro predeterminado si la jerarquía no es agregable).  
  
-   Los atributos no relacionados se mueven al miembro All (basado en la medida).  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta muestra cómo se puede usar la función ValidMeasure para invalidar el comportamiento de la propiedad IgnoreUnrelatedDimensions. En el cubo de Adventure Works, el grupo de medida Sales Targets tiene establecido IgnoreUnrelatedDimensions en False; dado que la dimensión Date se combina con este grupo de medida en la granularidad de Calendar Quarter, esto significa que la medida Sales Quota, de forma predeterminada, devolverá NULL por debajo de Calendar Quarter (aunque hay también un cálculo en el script MDX que asigna valores hasta el nivel Month). La función ValidMeasure se puede utilizar en una medida calculada para hacer que la medida Sales Quota se comporte como si IgnoreUnrelatedDimensions estuviera establecido en True y que Sales Quota muestre el valor de Calendar Quarter actual.  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 De igual forma, el grupo de medida Sales Targets no tiene ninguna relación con la dimensión de Promotion, de modo que por debajo de Todos los miembros de cualquier jerarquía se devolverá NULL. De nuevo, este comportamiento se puede cambiar con ValidMeasure:  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
