---
title: Correlación (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0140cc76a47df26ee42701152794f2ef9ec0f51e
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739744"
---
# <a name="correlation-mdx"></a>Correlation (MDX)


  Devuelve el coeficiente de correlación de los pares de valores X-Y evaluados sobre un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Correlation( Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression_y*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje Y.  
  
 *Numeric_Expression_x*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número que representa los valores del eje X.  
  
## <a name="remarks"></a>Notas  
 El **correlación** función calcula el coeficiente de correlación de dos pares de valores, evaluando primero el conjunto especificado con la primera expresión numérica para obtener los valores del eje y. La función, a continuación, evalúa el conjunto especificado con la segunda expresión numérica, si está presente, para obtener el conjunto de valores para el eje x. Si no se especifica la segunda expresión numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje X.  
  
> [!NOTE]  
>  El **correlación** función omite las celdas vacías o celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
