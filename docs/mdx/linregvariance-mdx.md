---
title: LinRegVariance (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LINREGVARIANCE
dev_langs:
- kbMDX
helpviewer_keywords:
- LinRegVariance function
ms.assetid: 09803510-2d71-401b-970e-bbdcac06558d
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 30ce6e0e7f43be71824734b7ab9790007a9f4763
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="linregvariance-mdx"></a>LinRegVariance (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Calcula la regresión lineal de un conjunto y devuelve la varianza asociada a la recta de regresión y = ax + b..  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

