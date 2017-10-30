---
title: LinRegSlope (MDX) | Documentos de Microsoft
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
- LINREGSLOPE
dev_langs:
- kbMDX
helpviewer_keywords:
- LinRegSlope function
ms.assetid: dc61f941-b25d-4eef-9b25-75e03a1dd6de
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 225c9be61c4403c9a52f61e89821c97193aa7756
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="linregslope-mdx"></a>LinRegSlope (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Calcula la regresión lineal de un conjunto y devuelve el valor de la pendiente de la recta de regresión y = ax + b..  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LinRegSlope(Set_Expression, Numeric_Expression_y [ ,Numeric_Expression_x ] )  
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
  
 El **LinRegSlope** función evalúa el conjunto especificado con la primera expresión numérica para obtener los valores del eje y. A continuación, la función evalúa la expresión de conjunto especificada con la segunda expresión numérica, si se especifica, para obtener los valores del eje X. Si no se especifica la segunda expresión numérica, la función utiliza el contexto actual de las celdas del conjunto especificado como valores para el eje X. No se especifica el argumento del eje x se suele usar con la dimensión de tiempo.  
  
 Después de obtener el conjunto de puntos, la **LinRegSlope** función devuelve la pendiente de la recta de regresión (una en la ecuación anterior).  
  
> [!NOTE]  
>  El **LinRegSlope** función omite las celdas vacías o celdas que contienen texto o valores lógicos. No obstante, la función incluye celdas con valor de cero.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la pendiente de una recta de regresión para las medidas de ventas por unidad y por tienda.  
  
```  
LinRegSlope(LastPeriods(10),[Measures].[Unit Sales],[Measures].[Store Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

