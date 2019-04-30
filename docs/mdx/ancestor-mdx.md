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
manager: kfile
ms.openlocfilehash: 464f8504850c6aa13f1cf040f9429be56f7181be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298499"
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
  
 *distancia*  
 Expresión numérica válida que especifica la distancia desde el miembro especificado.  
  
## <a name="remarks"></a>Comentarios  
 Con el **antecesor** función, se proporciona la función con una expresión de miembro MDX y, a continuación, se proporciona una expresión MDX de un nivel que sea un antecesor del miembro o una expresión numérica que representa el número de niveles por encima ese miembro. Con esta información, el **antecesores** función devuelve el miembro antecesor en ese nivel.  
  
> [!NOTE]  
>  Para devolver un conjunto que contiene el miembro antecesor, en lugar de simplemente el miembro antecesor, utilice el [antecesores &#40;MDX&#41; ](../mdx/ancestors-mdx.md) función.  
  
 Si se especifica una expresión de nivel, el **antecesor** función devuelve el antecesor del miembro especificado en el nivel especificado. Si el miembro especificado no se encuentra dentro de la misma jerarquía que el nivel especificado, la función devuelve un error.  
  
 Si se especifica una distancia, el **antecesor** función devuelve el antecesor del miembro especificado que es el número de pasos especificado hacia arriba en la jerarquía especificada por la expresión de miembro. Se puede especificar un miembro como miembro de una jerarquía de atributo, una jerarquía definida por el usuario o, en algunos casos, una jerarquía de elementos primarios y secundarios. El número 1 devuelve un elemento primario del miembro y el número 2 devuelve un elemento primario de segundo nivel (si existe) del miembro. El número 0 devuelve el propio miembro.  
  
> [!NOTE]  
>  Utilice este formulario de la **antecesor** función para los casos en que el nivel del elemento primario es desconocido o no se puede nombrar.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
