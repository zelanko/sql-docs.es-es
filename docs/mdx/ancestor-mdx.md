---
title: Antecesor (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 385206d4a94362831e0949bafe5a11c1ce48d7bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017127"
---
# <a name="ancestor-mdx"></a>Ancestor (MDX)


  Función que devuelve el antecesor de un miembro especificado en un nivel especificado o a una distancia especificada del miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Posición*  
 Expresión numérica válida que especifica la distancia desde el miembro especificado.  
  
## <a name="remarks"></a>Observaciones  
 Con la función **ancestor** , se proporciona la función con una expresión de miembro MDX y, a continuación, se proporciona una expresión MDX de un nivel que sea un antecesor del miembro o una expresión numérica que represente el número de niveles por encima de ese miembro. Con esta información, la función **ancestor** devuelve el miembro antecesor en ese nivel.  
  
> [!NOTE]  
>  Para devolver un conjunto que contenga el miembro antecesor, en lugar de solo el miembro antecesor, use los [antecesores &#40;función&#41;MDX](../mdx/ancestors-mdx.md) .  
  
 Si se especifica una expresión de nivel, la función **ancestor** devuelve el antecesor del miembro especificado en el nivel especificado. Si el miembro especificado no se encuentra dentro de la misma jerarquía que el nivel especificado, la función devuelve un error.  
  
 Si se especifica una distancia, la función **ancestor** devuelve el antecesor del miembro especificado que es el número de pasos especificados en la jerarquía especificada por la expresión de miembro. Se puede especificar un miembro como miembro de una jerarquía de atributo, una jerarquía definida por el usuario o, en algunos casos, una jerarquía de elementos primarios y secundarios. El número 1 devuelve un elemento primario del miembro y el número 2 devuelve un elemento primario de segundo nivel (si existe) del miembro. El número 0 devuelve el propio miembro.  
  
> [!NOTE]  
>  Use esta forma de la función **ancestor** para los casos en los que el nivel del elemento primario es desconocido o no se puede nombrar.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente utiliza una expresión de nivel y devuelve el valor Internet Sales Amount para cada State-Province de Australia, junto con su porcentaje del total de Internet Sales Amount para Australia.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
   [Measures].[Internet Sales Amount],    
      Ancestor   
         (  
         [Customer].[Customer Geography].CurrentMember,  
            [Customer].[Customer Geography].[Country]  
         )  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
        [Customer].[Customer Geography].[Country].&[Australia],  
           [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente utiliza una expresión numérica y devuelve Internet Sales Amount para cada State-Province de Australia, junto con su porcentaje del total de Internet Sales Amount para todos los países.  
  
```  
WITH MEMBER Measures.x AS [Measures].[Internet Sales Amount] /   
   (  
      [Measures].[Internet Sales Amount],  
         Ancestor   
            ([Customer].[Customer Geography].CurrentMember, 2)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{  
   Descendants   
      (  
         [Customer].[Customer Geography].[Country].&[Australia],  
            [Customer].[Customer Geography].[State-Province], SELF   
      )  
} ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
