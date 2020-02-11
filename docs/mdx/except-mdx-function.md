---
title: Except (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d53a88ce78eb5a1b106cefb0832ca1023f67c000
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077248"
---
# <a name="except-mdx-function"></a>Except (MDX), función


  Evalúa dos conjuntos y quita las tuplas del primer conjunto que también existen en el segundo conjunto; opcionalmente, conserva los duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Except(Set_Expression1, Set_Expression2 [, ALL ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica **All** , la función conserva los duplicados encontrados en el primer conjunto; los duplicados encontrados en el segundo conjunto se seguirán quitando. Los miembros se devuelven en el orden en que aparecen en el primer conjunto.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de esta función.  
  
```  
   //This query shows the quantity of orders for all products,  
   //with the exception of Components, which are not  
   //sold.  
SELECT   
   [Date].[Month of Year].Children  ON COLUMNS,  
   Except  
      ([Product].[Product Categories].[All].Children ,  
         {[Product].[Product Categories].[Components]}  
      ) ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   ([Measures].[Order Quantity])  
```  
  
## <a name="see-also"></a>Consulte también  
 [-&#40;excepto&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
