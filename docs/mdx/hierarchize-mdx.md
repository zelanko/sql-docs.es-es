---
title: Hierarchize (MDX) | Documentos de Microsoft
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
- HIERARCHIZE
dev_langs:
- kbMDX
helpviewer_keywords:
- Hierarchize function
ms.assetid: e9795003-70e7-4b4c-9074-45b5b9b817fa
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d0c093d032b587a8935d12c8234ab33da52ee86d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="hierarchize-mdx"></a>Hierarchize (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 El ejemplo siguiente reducirá el detalle del miembro Canadá. El **Hierarchize** función se utiliza para organizar los miembros de dicho conjunto en orden jerárquico, y es necesario para la **DrillUpMember** función.  
  
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
  
 En el ejemplo siguiente se devuelve la suma de la `Measures.[Order Quantity]` miembro, que se agrega en los primeros nueve meses de 2003 incluidos en el `Date` dimensión, desde el **Adventure Works** cubo. El **PeriodsToDate** función define las tuplas del conjunto en la que opera la función de agregado. El **Hierarchize** función organiza los miembros del conjunto especificado de miembros de la dimensión Product en orden jerárquico.  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

