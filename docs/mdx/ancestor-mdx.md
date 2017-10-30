---
title: Antecesor (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ANCESTOR
dev_langs:
- kbMDX
helpviewer_keywords:
- Ancestor function
ms.assetid: b5bf2ce4-20df-4ebc-97eb-e44a6f64cc50
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a9aad080913e792291f8d72281afe522704042e5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="ancestor-mdx"></a>Ancestor (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Función que devuelve el antecesor de un miembro especificado en un nivel especificado o a una distancia especificada del miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level syntax  
Ancestor(Member_Expression, Level_Expression)  
  
Numeric syntax  
Ancestor(Member_Expression, Distance)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Distancia*  
 Expresión numérica válida que especifica la distancia desde el miembro especificado.  
  
## <a name="remarks"></a>Comentarios  
 Con el **antecesor** función, se proporciona la función con una expresión de miembro MDX y, a continuación, se proporciona una expresión MDX de un nivel que sea un antecesor del miembro o una expresión numérica que representa el número de niveles por encima de ese miembro. Con esta información, el **antecesores** función devuelve el miembro antecesor en ese nivel.  
  
> [!NOTE]  
>  Para devolver un conjunto que contiene el miembro antecesor, en lugar de simplemente el miembro antecesor, utilice la [antecesores &#40; MDX &#41; ](../mdx/ancestors-mdx.md) (función).  
  
 Si se especifica una expresión de nivel, la **antecesor** función devuelve el antecesor del miembro especificado en el nivel especificado. Si el miembro especificado no se encuentra dentro de la misma jerarquía que el nivel especificado, la función devuelve un error.  
  
 Si se especifica una distancia, la **antecesor** función devuelve el antecesor del miembro especificado que corresponde al número de pasos especificado hacia arriba en la jerarquía especificada por la expresión de miembro. Se puede especificar un miembro como miembro de una jerarquía de atributo, una jerarquía definida por el usuario o, en algunos casos, una jerarquía de elementos primarios y secundarios. El número 1 devuelve un elemento primario del miembro y el número 2 devuelve un elemento primario de segundo nivel (si existe) del miembro. El número 0 devuelve el propio miembro.  
  
> [!NOTE]  
>  Utilice este formulario de la **antecesor** función para los casos en que el nivel del elemento primario es desconocido o no se puede llamar.  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

