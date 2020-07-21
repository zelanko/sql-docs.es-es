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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097374"
---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)


  Devuelve una cadena con formato de expresiones multidimensionales (MDX) que corresponde a una tupla especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
## <a name="remarks"></a>Observaciones  
 Esta función se utiliza para transferir una representación de cadena de una tupla a una función externa para su análisis. La cadena que se devuelve se incluye entre llaves {} y cada miembro, si se define explícitamente más de uno en la tupla, está separado por una coma.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve la cadena ([Date]. [ Calendar Year]. & [2001], [Geography]. [Geografía]. [País]. & [Estados Unidos]):  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
