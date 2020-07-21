---
title: Palabra clave EXISTing (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
ms.openlocfilehash: 115444c832fe8fe9b258a0c23b97b97553f32e8e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546217"
---
# <a name="existing-keyword-mdx"></a>EXISTING (Palabra clave, MDX)
  Exige que un conjunto especificado se evalúe en el contexto actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Una expresión de conjunto de MDX (Expresiones multidimensionales) válida.  
  
## <a name="remarks"></a>Observaciones  
 De forma predeterminada, los conjuntos se evalúan en el contexto del cubo que contiene los miembros del conjunto. La palabra clave `Existing` fuerza a un conjunto especificado a evaluarse en el contexto actual.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el recuento de los distribuidores cuyas ventas han disminuido en el período de tiempo anterior, de acuerdo con los valores de los miembros State-Province seleccionados por el usuario, evaluados mediante la función `Aggregate`. La palabra clave [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) y [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) se usan para devolver valores para las ventas que han disminuido en las categorías de productos de la dimensión Product. La `Existing` palabra clave obliga al conjunto de la `Filter` función a evaluarse en el contexto actual, es decir, para los miembros de Washington y Oregon de la jerarquía de atributo State-provincia.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Count &#40;establecer&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [&#41;AddCalculatedMembers &#40;MDX](/sql/mdx/addcalculatedmembers-mdx)   
 [&#40;de&#41;MDX de agregado](/sql/mdx/aggregate-mdx)   
 [Filtrar &#40;&#41;MDX](/sql/mdx/filter-mdx)   
 [Propiedades &#40;&#41;MDX](/sql/mdx/properties-mdx)   
 [&#41;DrilldownLevel &#40;MDX](/sql/mdx/drilldownlevel-mdx)   
 [Jerarquía &#40;&#41;MDX](/sql/mdx/hierarchize-mdx)   
 [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
