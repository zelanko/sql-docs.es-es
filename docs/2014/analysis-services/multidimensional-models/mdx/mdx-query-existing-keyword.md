---
title: EXISTING, palabra clave (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a781fb58f45c478b6a3611132a210b14012ffb72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228395"
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
  
## <a name="remarks"></a>Notas  
 De forma predeterminada, los conjuntos se evalúan en el contexto del cubo que contiene los miembros del conjunto. El `Existing` palabra clave fuerza a un conjunto especificado a evaluarse en el contexto actual en su lugar.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el recuento de los distribuidores cuyas ventas han disminuido en el período de tiempo anterior, de acuerdo con los valores de los miembros State-Province seleccionados por el usuario, evaluados mediante la función `Aggregate`. La palabra clave [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) y [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) se usan para devolver valores para las ventas que han disminuido en las categorías de productos de la dimensión Product. El `Existing` obliga a la palabra clave el el conjunto en el `Filter` función va a evaluar en el contexto actual, es decir, para los miembros Washington y Oregon de la jerarquía de atributo State-Province.  
  
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
 [Recuento &#40;establecer&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [Agregado &#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [Filtro &#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [Propiedades &#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
