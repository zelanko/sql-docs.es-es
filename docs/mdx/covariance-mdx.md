---
description: Covariance (MDX)
title: Covarianza (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 32471a48f0a669f7b72b5946f07403d6851dfb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500538"
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
  
## <a name="remarks"></a>Observaciones  
 La función **covarianza** evalúa el conjunto especificado con la primera expresión numérica para obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la segunda expresión numérica, si se especifica, para obtener el conjunto de valores del eje X. Si no se especifica la segunda expresión numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje X.  
  
 La función de **covarianza** utiliza la fórmula de población sesgada. Esto contrasta con la función de la [covarianza](../mdx/covariancen-mdx.md) a la que utiliza la fórmula de población no sesgada (dividiendo el número de pares x-y y restando 1).  
  
> [!NOTE]  
>  La función **covarianza** omite las celdas vacías o las celdas que contienen texto o los valores lógicos se omiten. No obstante, la función incluye celdas con valor de cero.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
