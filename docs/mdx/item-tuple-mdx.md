---
title: Elemento (tupla) (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 18217c0798155c912baa6afa30b33f5533a0e198
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579467"
---
# <a name="item-tuple-mdx"></a>Item (Tuple) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve una tupla desde un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Index syntax  
Set_Expression.Item(Index)  
  
String expression syntax  
Set_Expression.Item(String_Expression1 [ ,String_Expression2,...n])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Expression1*  
 Expresión de cadena válida que suele ser una tupla expresada en una cadena.  
  
 *Expression2*  
 Expresión de cadena válida que suele ser una tupla expresada en una cadena.  
  
 *Index*  
 Expresión numérica válida que especifica la tupla concreta mediante la posición dentro del conjunto que se devolverá.  
  
## <a name="remarks"></a>Notas  
 El **elemento** función devuelve una tupla del conjunto especificado. Hay tres formas de llamar a la **elemento** función:  
  
-   Si se especifica una expresión de cadena único, el **elemento** función devuelve la tupla especificada. Por ejemplo, "([2005].Q3, [Store05])".  
  
-   Si se especifica más de una expresión de cadena, la **elemento** función devuelve la tupla definida por las coordenadas especificadas. El número de cadenas debe coincidir con el número de ejes y cada cadena deben identificar una jerarquía única. Por ejemplo, "[2005].Q3", "[Store05]".  
  
-   Si se especifica un entero, el **elemento** función devuelve la tupla que se encuentra en la posición de base cero especificada por *índice*.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve ([1996],Sales):  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 El ejemplo siguiente utiliza una expresión de nivel y devuelve el valor Internet Sales Amount para cada State-Province de Australia, junto con su porcentaje del total de Internet Sales Amount para Australia. Este ejemplo utiliza la función Item para extraer la primera (y única tupla) del conjunto devuelto por la **antecesores** función.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],    
      Ancestors   
      ( [Customer].[Customer Geography].CurrentMember,  
        [Customer].[Customer Geography].[Country]  
      ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{ Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],  
     [Customer].[Customer Geography].[State-Province], SELF   
   )   
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
