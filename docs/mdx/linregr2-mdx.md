---
title: LinRegR2 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 42c703e703e8c557b4de8466a0cd1b686217fd4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63136207"
---
# <a name="linregr2-mdx"></a>LinRegR2 (MDX)


  Calcula la regresión lineal de un conjunto y devuelve el coeficiente de determinación, R<sup>2</sup>.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LinRegR2(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 El **LinRegR2** función evalúa el setagainst especificada la primera expressionto numérico obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la segunda expresión numérica, si se especifica, para obtener los valores del eje X. Si no especifica el segundo expressionis numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje x. No se especifica el x-axisargument se suele usar con la dimensión de tiempo.  
  
 Después de obtener el conjunto de puntos, la **LinRegR2** función devuelve el R estadístico<sup>2</sup> que describe el ajuste de la ecuación lineal a los puntos.  
  
> [!NOTE]  
>  El **LinRegR2** función la omite las celdas vacías o las celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el objeto estadístico R<sup>2</sup> que describe la adecuación de la ecuación de regresión lineal a los puntos de las ventas por unidad y las medidas de ventas de tienda.  
  
```  
LinRegR2(LastPeriods(10), [Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
