---
title: LinRegVariance (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b3ae56238623c41d29ccb388a5aaa178352af196
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208749"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)


  Calcula la regresión lineal de un conjunto y devuelve la varianza asociada a la recta de regresión y = ax + b.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LinRegVariance(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression_y*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje Y.  
  
 *Numeric_Expression_x*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje X.  
  
## <a name="remarks"></a>Comentarios  
 La regresión lineal, que utiliza el método de mínimos cuadrados, calcula la ecuación de la recta de regresión (es decir, la de mejor ajuste para un conjunto de puntos). La recta de regresión tiene la siguiente ecuación, donde una es la pendiente y b es la intersección:  
  
 y = ax+b  
  
 El **LinRegVariance** función evalúa el setagainst especificada la primera expresión numérica para obtener los valores del eje y. La función, a continuación, evalúa el setagainst especificado la expresión numérica en segundo lugar, si se especifica, para obtener los valores del eje x. Si no especifica el segundo expressionis numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje x. No se especifica el argumento del eje x se suele usar con la dimensión de tiempo.  
  
 Después de obtener el conjunto de puntos, la **LinRegVariance** función devuelve la varianza estadística que describe el ajuste de la ecuación lineal a los puntos.  
  
> [!NOTE]  
>  El **LinRegVariance** función la omite las celdas vacías o las celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la varianza estadística que describe la adecuación de la ecuación lineal a los puntos de las medidas de ventas por unidad y ventas por tienda.  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
