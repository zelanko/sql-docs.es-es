---
title: Covarianza (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COVARIANCE
dev_langs: kbMDX
helpviewer_keywords: Covariance function
ms.assetid: 5faf6742-62db-4c5c-8797-096bf1cab273
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3a00d12c88df72dda0d7c0d929c8e3b99ff77f6e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="covariance-mdx"></a>Covariance (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 El **covarianza** función evalúa el conjunto especificado con la primera expresión numérica, para obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la segunda expresión numérica, si se especifica, para obtener el conjunto de valores del eje X. Si no se especifica el segundo expressionis numérico, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje x.  
  
 El **covarianza** función utiliza la fórmula de población sesgada. Se trata de diferencia el [CovarianceN](../mdx/covariancen-mdx.md) función que utiliza la fórmula de población no sesgada (dividiendo el número de pares x-y, a continuación, restar 1).  
  
> [!NOTE]  
>  El **covarianza** función omite las celdas vacías o celdas que contienen texto o valores lógicos se omiten. No obstante, la función incluye celdas con valor de cero.  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
