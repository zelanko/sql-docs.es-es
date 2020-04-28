---
title: Count (Set) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68047295"
---
# <a name="count-set-mdx"></a>Count (Set) (MDX)


  Devuelve el número de celdas de un conjunto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Observaciones  
 La función **Count (Set)** incluye o excluye celdas vacías, dependiendo de la sintaxis utilizada. Si se usa la sintaxis estándar, las celdas vacías se pueden excluir o incluir mediante las marcas **EXCLUDEEMPTY** o **INCLUDEEMPTY** , respectivamente. Si se utiliza la sintaxis alternativa, la función incluye siempre celdas vacías.  
  
 Para excluir las celdas vacías en el recuento de un conjunto, use la sintaxis estándar y la marca **EXCLUDEEMPTY** opcional.  
  
> [!NOTE]  
>  La función **Count (Set)** cuenta las celdas vacías de forma predeterminada. En cambio, la función **Count** de OLE DB que cuenta un conjunto excluye las celdas vacías de forma predeterminada.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente cuenta el número de celdas del conjunto de miembros que consta del elemento secundario de la jerarquía de atributo Model Name de la dimensión Product.  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se cuenta el número de productos de la dimensión Product mediante la función **DrilldownLevel** junto con la función **Count** .  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 En el ejemplo siguiente se devuelven los revendedores con ventas declinadas en comparación con el trimestre natural anterior, mediante la función **Count** junto con la función **Filter** y otras funciones. Esta consulta usa la función de **agregado** para admitir la selección de varios miembros de geografía, como para la selección desde una lista desplegable en una aplicación cliente.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Recuento &#40;dimensión&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [Recuento &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [Count &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [&#41;DrilldownLevel &#40;MDX](../mdx/drilldownlevel-mdx.md)   
 [&#41;AddCalculatedMembers &#40;MDX](../mdx/addcalculatedmembers-mdx.md)   
 [Jerarquía &#40;&#41;MDX](../mdx/hierarchize-mdx.md)   
 [Propiedades &#40;&#41;MDX](../mdx/properties-mdx.md)   
 [&#40;de&#41;MDX de agregado](../mdx/aggregate-mdx.md)   
 [Filtrar &#40;&#41;MDX](../mdx/filter-mdx.md)   
 [&#41;PrevMember &#40;MDX](../mdx/prevmember-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
