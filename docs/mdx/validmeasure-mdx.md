---
title: ValidMeasure (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b3bce4baf3dc3499621f67defd40a4579e9cd460
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037956"
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)


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
  
 El comportamiento especificado por esta función es el comportamiento de servidor predeterminado y se controla mediante el **IgnoreUnrelatedDimensions** propiedad del objeto de grupo de medida.  
  
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
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
