---
title: EXISTING, palabra clave (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5078aa14be3c476e8b89545ed1541f12b7686f4e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-query---existing-keyword"></a>Consulta MDX - EXISTING, palabra clave
  Exige que un conjunto especificado se evalúe en el contexto actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Una expresión de conjunto de MDX (Expresiones multidimensionales) válida.  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, los conjuntos se evalúan en el contexto del cubo que contiene los miembros del conjunto. La palabra clave **Existing** fuerza a un conjunto especificado a evaluarse en el contexto actual.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el recuento de los distribuidores cuyas ventas han disminuido en el período de tiempo anterior, según los valores de los miembros State-Province seleccionados por el usuario y evaluados con la función **Aggregate** . La palabra clave [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md) y [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) se usan para devolver valores para las ventas que han disminuido en las categorías de productos de la dimensión Product. La palabra clave **Existing** fuerza al conjunto de la función **Filter** a que se evalúe en el contexto actual, es decir, para los miembros Washington y Oregon de la jerarquía de atributo State-Province.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40; MDX &#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Agregado &#40; MDX &#41;](../../../mdx/aggregate-mdx.md)   
 [Filtro &#40; MDX &#41;](../../../mdx/filter-mdx.md)   
 [Propiedades &#40; MDX &#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40; MDX &#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize &#40; MDX &#41;](../../../mdx/hierarchize-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  

