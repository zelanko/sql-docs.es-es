---
title: Item (tupla) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5740095752b482430cd718d0e2bff813449d92ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105222"
---
# <a name="item-tuple-mdx"></a>Item (Tuple) (MDX)


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
  
 *String_Expression1*  
 Expresión de cadena válida que suele ser una tupla expresada en una cadena.  
  
 *String_Expression2*  
 Expresión de cadena válida que suele ser una tupla expresada en una cadena.  
  
 *Ajustar*  
 Expresión numérica válida que especifica la tupla concreta mediante la posición dentro del conjunto que se devolverá.  
  
## <a name="remarks"></a>Observaciones  
 La función **Item** devuelve una tupla del conjunto especificado. Hay tres formas posibles de llamar a la función **Item** :  
  
-   Si se especifica una expresión de cadena única, la función **Item** devuelve la tupla especificada. Por ejemplo, "([2005].Q3, [Store05])".  
  
-   Si se especifica más de una expresión de cadena, la función **Item** devuelve la tupla definida por las coordenadas especificadas. El número de cadenas debe coincidir con el número de ejes y cada cadena deben identificar una jerarquía única. Por ejemplo, "[2005].Q3", "[Store05]".  
  
-   Si se especifica un entero, la función **Item** devuelve la tupla que se encuentra en la posición de base cero especificada por *index*.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve ([1996],Sales):  
  
 `{([1996],Sales), ([1997],Sales), ([1998],Sales)}.Item(0)`  
  
 El ejemplo siguiente utiliza una expresión de nivel y devuelve el valor Internet Sales Amount para cada State-Province de Australia, junto con su porcentaje del total de Internet Sales Amount para Australia. En este ejemplo se usa la función Item para extraer la primera (y solo tupla) del conjunto devuelto por la función **antecesores** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
