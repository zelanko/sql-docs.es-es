---
description: PrevMember (MDX)
title: PrevMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f02dfca925fce4399bb9f0c4a8c7ff1e005e598
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471667"
---
# <a name="prevmember-mdx"></a>PrevMember (MDX)


  Devuelve el miembro anterior en el nivel que contiene un miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.PrevMember   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **PrevMember** devuelve el miembro anterior en el mismo nivel que el miembro especificado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra una consulta simple que utiliza la función **PrevMember** para mostrar el nombre del miembro inmediatamente antes del miembro actual en el eje Rows:  
  
 `WITH MEMBER MEASURES.PREVMEMBERDEMO AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.PREVMEMBER.NAME`  
  
 `SELECT MEASURES.PREVMEMBERDEMO ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 El ejemplo siguiente devuelve el recuento de los distribuidores cuyas ventas han disminuido en el período de tiempo anterior, de acuerdo con los valores de los miembros State-Province seleccionados por el usuario evaluados mediante la función Aggregate. Las funciones **Hierarchy** y **DrillDownLevel** se utilizan para devolver valores para las ventas que se rechazan para las categorías de producto de la dimensión product. La función **PrevMember** se usa para comparar el período de tiempo actual con el período de tiempo anterior.  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS   
   Count(  
      Filter(  
         Existing(Reseller.Reseller.Reseller),   
            [Measures].[Reseller Sales Amount] < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
            )  
         )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate (   
      {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
         )  
SELECT NON EMPTY Hierarchize (  
   AddCalculatedMembers (  
      {DrillDownLevel({[Product].[All Products]})}  
         )  
   )  
        DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,   
    [Date].[Calendar].[Calendar Quarter].&[2003]&[4],  
    [Measures].[Declining Reseller Sales])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
