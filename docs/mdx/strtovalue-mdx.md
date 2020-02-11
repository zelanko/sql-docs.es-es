---
title: StrToValue (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cad8fec605a56a60cfcc7024739225e474fd42f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036691"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  Devuelve el valor numérico especificado por una cadena con formato de expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *MDX_Expression*  
 Expresión de cadena válida que se resuelve, directa o indirectamente, en una sola celda.  
  
## <a name="remarks"></a>Observaciones  
 La función **StrToValue** devuelve el valor numérico especificado por la expresión MDX. La función **StrToValue** se utiliza normalmente con funciones definidas por el usuario para devolver una expresión MDX de una función externa a una instrucción MDX que se puede resolver en una sola celda.  
  
-   Cuando se utiliza la marca CONSTRAINED, la expresión MDX debe contener solo un valor escalar. La marca CONSTRAINED se utiliza para reducir el riesgo de ataques por inyección de código mediante la cadena especificada. Si se proporciona una expresión MDX que no se resuelve directamente en un valor escalar, aparece el siguiente error: "Se infringieron las restricciones impuestas por la marca CONSTRAINED en la función STRTOVALUE."  
  
-   Cuando no se utiliza la marca CONSTRAINED, la expresión MDX especificada puede ser tan compleja como se desee, siempre que se resuelva en una expresión MDX (Expresiones multidimensionales) válida que devuelva una única celda.  
  
> [!NOTE]  
>  La devolución del resultado de una expresión MDX como un valor numérico puede ser útil si el valor se almacena como texto y se desean realizar operaciones aritméticas con los valores devueltos.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa la función **StrToValue** para devolver el peso de cada bicicleta como un valor.  
  
```  
WITH MEMBER Measures.x AS   
StrToValue   
   ([Product].[Product].CurrentMember.Properties ('Weight')  
   ,CONSTRAINED  
   )  
SELECT Measures.x ON 0  
,[Product].[Product].[Product].Members ON 1  
FROM [Adventure Works]  
WHERE [Product].[Product Categories].[Bikes]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
