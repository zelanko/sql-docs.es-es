---
description: Hierarchize (MDX)
title: Jerarquía (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3c1683819420d150e2f9b330ba94bc9e228d167f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429917"
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
  
## <a name="remarks"></a>Observaciones  
 La función **Hierarchy** organiza los miembros del conjunto especificado en orden jerárquico. La función siempre conserva los duplicados.  
  
-   Si no se especifica **post** , la función ordena los miembros de un nivel en su orden natural. Su orden natural es la clasificación predeterminada de los miembros en la jerarquía cuando no se especifican otras condiciones de clasificación. Los miembros secundarios se sitúan inmediatamente después de sus respectivos miembros primarios.  
  
-   Si se especifica **post** , la función **Hierarchy** ordena los miembros en un nivel mediante un orden posterior. Es decir, los miembros secundarios preceden a los miembros primarios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente reducirá el detalle del miembro Canadá. La función **Hierarchy** se usa para organizar los miembros de conjuntos especificados en orden jerárquico, que es necesario para la función **DrillUpMember** .  
  
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
  
 En el ejemplo siguiente se devuelve la suma del `Measures.[Order Quantity]` miembro, agregada durante los primeros nueve meses de 2003 contenidos en la `Date` dimensión, del cubo **Adventure Works** . La función **PeriodsToDate** define las tuplas en el conjunto sobre el que funciona la función de agregado. La función **Hierarchy** organiza los miembros del conjunto de miembros especificado de la dimensión Product en orden jerárquico.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
