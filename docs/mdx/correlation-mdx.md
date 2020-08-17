---
description: Correlation (MDX)
title: Correlación (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ae050b681830b81ffa63ae82c714d69d54b03c91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387651"
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
  
## <a name="remarks"></a>Observaciones  
 La función de **correlación** calcula el coeficiente de correlación de dos pares de valores al evaluar primero el conjunto especificado con la primera expresión numérica para obtener los valores del eje y. A continuación, la función evalúa el conjunto especificado con la segunda expresión numérica, si está presente, para obtener el conjunto de valores del eje x. Si no se especifica la segunda expresión numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje X.  
  
> [!NOTE]  
>  La función de **correlación** omite las celdas vacías o las celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
