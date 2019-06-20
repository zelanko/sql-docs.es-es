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
manager: kfile
ms.openlocfilehash: c327dc55420cc89f5e76b6fae7822fad3a4e95f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63136109"
---
# <a name="strtovalue-mdx"></a>StrToValue (MDX)


  Devuelve el valor numérico especificado por una cadena con formato de expresiones multidimensionales MDX.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToValue(MDX_Expression [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *MDX_Expression*  
 Expresión de cadena válida que se resuelve, directa o indirectamente, en una sola celda.  
  
## <a name="remarks"></a>Comentarios  
 El **StrToValue** función devuelve el valor numérico especificado por la expresión MDX. El **StrToValue** función normalmente se utiliza con funciones definidas por el usuario para devolver una expresión MDX desde una función externa a una instrucción MDX que se puede resolver en una sola celda.  
  
-   Cuando se utiliza la marca CONSTRAINED, la expresión MDX debe contener solo un valor escalar. La marca CONSTRAINED se utiliza para reducir el riesgo de ataques por inyección de código mediante la cadena especificada. Si una expresión MDX es siempre no sea de resolverse directamente en un valor escalar, aparece el siguiente error: "Las restricciones impuestas por la CONSTRAINED se han infringido la marca en la función STRTOVALUE."  
  
-   Cuando no se utiliza la marca CONSTRAINED, la expresión MDX especificada puede ser tan compleja como se desee, siempre que se resuelva en una expresión MDX (Expresiones multidimensionales) válida que devuelva una única celda.  
  
> [!NOTE]  
>  La devolución del resultado de una expresión MDX como un valor numérico puede ser útil si el valor se almacena como texto y se desean realizar operaciones aritméticas con los valores devueltos.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el **StrToValue** función para devolver el peso de cada bicicleta como un valor.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
