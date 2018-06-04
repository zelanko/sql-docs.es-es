---
title: LinRegVariance (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 314937dce7f423e2ca57183a9686c0059b2d2970
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579237"
---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Notas  
 La regresión lineal, que utiliza el método de mínimos cuadrados, calcula la ecuación de la recta de regresión (es decir, la de mejor ajuste para un conjunto de puntos). La recta de regresión tiene la siguiente ecuación, donde una es la pendiente y b es la intersección:  
  
 y = ax+b  
  
 El **LinRegVariance** función evalúa el setagainst especificado la primera expresión numérica para obtener los valores del eje y. La función, a continuación, evalúa el setagainst especificado la expresión numérica en segundo lugar, si se especifica, para obtener los valores del eje x. Si no se especifica el segundo expressionis numérico, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje x. No se especifica el argumento del eje x se suele usar con la dimensión de tiempo.  
  
 Después de obtener el conjunto de puntos, la **LinRegVariance** función devuelve la varianza estadística que describe el ajuste de la ecuación lineal a los puntos.  
  
> [!NOTE]  
>  El **LinRegVariance** función omite las celdas vacías o celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la varianza estadística que describe la adecuación de la ecuación lineal a los puntos de las medidas de ventas por unidad y ventas por tienda.  
  
```  
LinRegVariance(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
