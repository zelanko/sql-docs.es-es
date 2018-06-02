---
title: CovarianceN (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 061a444fbc08406ac7b4d1f300d9238141afcb89
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578767"
---
# <a name="covariancen-mdx"></a>CovarianceN (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve la covarianza de ejemplo de los pares de valores X-Y evaluados sobre un conjunto mediante la fórmula de población no sesgada (al dividir por el número de pares X-Y).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CovarianceN(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression_y*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje Y.  
  
 *Numeric_Expression_x*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje X.  
  
## <a name="remarks"></a>Notas  
 El **CovarianceN** función evalúa el conjunto especificado con la primera expresión numérica, para obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la segunda expresión numérica, si se especifica, para obtener el conjunto de valores del eje X. Si no se especifica la segunda expresión numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje x.  
  
 El **CovarianceN** función utiliza la fórmula de población no sesgada. Se trata de diferencia el [covarianza](../mdx/covariance-mdx.md) función que utiliza la fórmula de población sesgada (al dividir por el número de pares x-y).  
  
> [!NOTE]  
>  El **CovarianceN** función omite las celdas vacías o celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
