---
title: Covarianza (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1bb24e4dcb536af144214f96dd5b904cc8530cd4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249605"
---
# <a name="covariance-mdx"></a>Covariance (MDX)


  Devuelve la covarianza de población de los pares de valores X-Y evaluados sobre un conjunto mediante la fórmula de población sesgada (al dividir por el número de pares X-Y).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Covariance(Set_Expression,Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression_y*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje Y.  
  
 *Numeric_Expression_x*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje X.  
  
## <a name="remarks"></a>Comentarios  
 El **covarianza** función evalúa el conjunto especificado con la primera expresión numérica para obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la segunda expresión numérica, si se especifica, para obtener el conjunto de valores del eje X. Si no especifica el segundo expressionis numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje x.  
  
 El **covarianza** función utiliza la fórmula de población sesgada. Esto es por el contrario el [CovarianceN](../mdx/covariancen-mdx.md) función que utiliza la fórmula de población no sesgada (al dividir el número de pares x-y, a continuación, restar 1).  
  
> [!NOTE]  
>  El **covarianza** se omiten los valores lógicos o función la omite las celdas vacías o las celdas que contienen texto. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo usar la función Covariance:  
  
```  
WITH   
MEMBER [Measures].[CovarianceDemo] AS  
COVARIANCE([Date].[Date].[Date].Members, [Measures].[Internet Sales Amount], [Measures].[Internet Order Count])   
SELECT {[Measures].[CovarianceDemo]} ON 0   
FROM  
[Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
