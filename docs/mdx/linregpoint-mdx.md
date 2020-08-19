---
description: LinRegPoint (MDX)
title: LinRegPoint (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4f298d58b14f3005b86f8fa7773a4faef1c94c79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429847"
---
# <a name="linregpoint-mdx"></a>LinRegPoint (MDX)


  Calcula la regresión lineal de un conjunto y devuelve el valor de la *intersección de y* en la línea de regresión, y = AX + b para un valor determinado de x.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LinRegPoint(Slice_Expression_x, Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Slice_Expression_x*  
 Expresión numérica válida que suele ser una expresión MDX (Expresiones multidimensionales) de las coordenadas de celdas que devuelven un número que representa los valores del eje segmentador.  
  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression_y*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje Y.  
  
 *Numeric_Expression_x*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje X.  
  
## <a name="remarks"></a>Observaciones  
 La regresión lineal, que utiliza el método de mínimos cuadrados, calcula la ecuación de la recta de regresión (es decir, la de mejor ajuste para un conjunto de puntos). La línea de regresión tiene la siguiente ecuación, donde a es la pendiente y b es la intercepción:  
  
 y = ax+b  
  
 La función **LinRegPoint** evalúa el conjunto especificado con la segunda expresión numérica para obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la tercera expresión numérica, si se especifica, para obtener los valores del eje X. Si no se especifica la tercera expresión numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje X. La no especificación del argumento del eje x se usa con frecuencia con la dimensión de tiempo.  
  
 Una vez que se ha calculado la recta de regresión lineal, se calcula el valor de la ecuación para la primera expresión numérica y, a continuación, se devuelve.  
  
> [!NOTE]  
>  La función **LinRegPoint** omite las celdas vacías o las celdas que contienen texto. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor predicho de las ventas por unidad de los últimos diez períodos según la relación estadística entre Unit Sales y Store Sales.  
  
```  
LinRegPoint([Measures].[Unit Sales],LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
