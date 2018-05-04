---
title: EXISTING, palabra clave (MDX) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 888c3039c98b36b15f28f6cfac21506547f3940c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-query---existing-keyword"></a>Consulta MDX - EXISTING, palabra clave
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Número de & #40; Conjunto de & #41; & #40; MDX & #41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers & #40; MDX & #41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [Agregado & #40; MDX & #41;](../../../mdx/aggregate-mdx.md)   
 [Filtro & #40; MDX & #41;](../../../mdx/filter-mdx.md)   
 [Propiedades & #40; MDX & #41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel & #40; MDX & #41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize & #40; MDX & #41;](../../../mdx/hierarchize-mdx.md)   
 [Referencia de funciones MDX & #40; MDX & #41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
