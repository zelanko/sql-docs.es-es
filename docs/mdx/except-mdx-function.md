---
title: Excepto (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03d9b5140eb0cbf9d868e43c65213efe917994a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690879"
---
# <a name="except-mdx-function"></a>EXCEPT, función (MDX)


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
  
## <a name="remarks"></a>Comentarios  
 Si **todas** está especificado, la función conserva los duplicados se encuentra en el primer conjunto; duplicados encontrados en el segundo conjunto se quitarán. Los miembros se devuelven en el orden en que aparecen en el primer conjunto.  
  
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
  
## <a name="see-also"></a>Vea también  
 [- &#40;Except&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
