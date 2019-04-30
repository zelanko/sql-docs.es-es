---
title: Hierarchize (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4478fb9657ef4577bcae8b5641f53154b2a0486c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224905"
---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)


  Ordena los miembros de un conjunto en una jerarquía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Hierarchize(Set_Expression [ , POST ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **Hierarchize** función organiza los miembros del conjunto especificado en un orden jerárquico. La función siempre conserva los duplicados.  
  
-   Si **POST** no se especifica, la función ordena los miembros de un nivel en su orden natural. Su orden natural es la clasificación predeterminada de los miembros en la jerarquía cuando no se especifican otras condiciones de clasificación. Los miembros secundarios se sitúan inmediatamente después de sus respectivos miembros primarios.  
  
-   Si **POST** se especifica, el **Hierarchize** función ordena los miembros en un nivel siguiendo un orden POST-natural. Es decir, los miembros secundarios preceden a los miembros primarios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente reducirá el detalle del miembro Canadá. El **Hierarchize** función se utiliza para organizar los miembros de dicho conjunto en orden jerárquico, que es necesaria para la **DrillUpMember** función.  
  
```  
SELECT DrillUpMember   
   (  
      Hierarchize  
         (  
            {[Geography].[Geography].[Country].[Canada]  
            ,[Geography].[Geography].[Country].[United States]  
            ,[Geography].[Geography].[State-Province].[Alberta]  
            ,[Geography].[Geography].[State-Province].[Brunswick]  
            ,[Geography].[Geography].[State-Province].[Colorado]   
            }  
         ), {[Geography].[Geography].[Country].[United States]}  
   )  
ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve la suma de los `Measures.[Order Quantity]` miembro, se agregan durante los primeros nueve meses de 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo. El **PeriodsToDate** función define las tuplas del conjunto en la que opera la función de agregado. El **Hierarchize** función organiza los miembros del conjunto especificado de miembros de la dimensión Product en orden jerárquico.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS Count  
   (Filter  
      (Existing  
         (Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] <   
               ([Measures].[Reseller Sales Amount],[Date].Calendar.PrevMember)  
        )  
    )  
MEMBER [Geography].[State-Province].x AS Aggregate   
( {[Geography].[State-Province].&[WA]&[US],   
   [Geography].[State-Province].&[OR]&[US] }   
)  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})}  
        )  
    ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
   [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
