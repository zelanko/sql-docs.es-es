---
title: TupleToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d6cde1f60274d1437517d89e48b111e9e7298b9d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097374"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  Devuelve una cadena con formato de expresiones multidimensionales MDX que corresponde a una tupla especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
## <a name="remarks"></a>Comentarios  
 Esta función se utiliza para transferir una representación de cadena de una tupla a una función externa para su análisis. La cadena devuelta aparece encerrado entre llaves {} y cada miembro, si más de uno expresamente definido en la tupla, está separado por punto y coma.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la cadena ([Date]. [ Año natural]. & [2001], [Geography]. [Geography]. [Country]. & [United States]):  
  
```  
WITH MEMBER Measures.x AS TupleToStr   
   (   
      ([Date].[Calendar Year].&[2001]  
         , [Geography].[Geography].[Country].&[United States]  
      )  
   )     
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve la misma cadena que el ejemplo anterior.  
  
```  
WITH SET s AS   
   {  
      ([Date].[Calendar Year].&[2001],  
         [Geography].[Geography].[Country].&[United States]  
      )   
   }  
MEMBER Measures.x AS TupleToStr ( s.Item(0) )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
