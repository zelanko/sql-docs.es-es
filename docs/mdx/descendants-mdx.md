---
description: Descendants (MDX)
title: Descendientes (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b883d1ce73a7259b285748e5a66f283a7d830424
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491444"
---
# <a name="descendants-mdx"></a>Descendants (MDX)


  Devuelve el conjunto de descendientes de un miembro en el nivel o distancia especificados; opcionalmente puede incluir o excluir los descendientes de otros niveles.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Distancia*  
 Expresión numérica válida que especifica la distancia desde el miembro especificado.  
  
 *Desc_Flag*  
 Expresión de cadena válida que especifica una marca de descripción que distingue entre posibles conjuntos de descendientes.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un nivel, la función **Descendants** devuelve un conjunto que contiene los descendientes del miembro especificado o los miembros del conjunto especificado, en un nivel especificado, modificado opcionalmente por una marca especificada en *Desc_Flag*.  
  
 Si se especifica *Distance* , la función **Descendants** devuelve un conjunto que contiene los descendientes del miembro especificado o los miembros del conjunto especificado que son el número especificado de niveles en la jerarquía del miembro especificado, modificado opcionalmente mediante una marca especificada en *Desc_Flag*. Esta función se suele utilizar con el argumento Distance para tratar con jerarquías desiguales. Si la distancia especificada es cero (0), la función devuelve un conjunto que consta solamente del miembro especificado o el conjunto especificado.  
  
 Si se especifica una expresión de conjunto, la función **Descendants** se resuelve individualmente para cada miembro del conjunto y se vuelve a crear el conjunto. En otras palabras, la sintaxis que se usa para la función **Descendants** es funcionalmente equivalente a la función [Generate](../mdx/generate-mdx.md) de MDX.  
  
 Si no se especifica ningún nivel o distancia, el valor predeterminado para el nivel utilizado por la función se determina mediante una llamada a la función [LEVEL](../mdx/level-mdx.md) (<\<Member>>. Nivel) para el miembro especificado (si se especifica un miembro) o mediante una llamada a la función **LEVEL** para cada miembro del conjunto especificado (si se especifica un conjunto). Si no se especifican una expresión de nivel, una distancia o marcas, la función tiene el mismo efecto que el uso de la sintaxis siguiente:  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 Si se especifica un nivel y no se especifica una marca de descripción, la función tiene el mismo efecto que el uso de la sintaxis siguiente.  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 Mediante la modificación del valor de la marca de descripción, puede incluir o excluir descendientes en el nivel o distancia especificados, el elemento secundario anterior o posterior al nivel o distancia especificados (hasta el nodo hoja), así como los elementos secundarios hoja, independientemente del nivel o distancia especificados. En la tabla siguiente se describen las marcas permitidas en el argumento *Desc_Flag* .  
  
|Marca|Descripción|  
|----------|-----------------|  
|SELF|Devuelve solo los miembros descendientes desde el nivel especificado o a la distancia especificada. La función incluye el miembro especificado si el nivel especificado es el del miembro especificado.|  
|AFTER|Devuelve los miembros descendientes de todos los niveles subordinados al nivel o distancia especificados.|  
|BEFORE|Devuelve los miembros descendientes de todos los niveles entre el miembro especificado y el nivel especificado, o a la distancia especificada. Incluye el miembro especificado, pero no incluye miembros del nivel o la distancia especificados.|  
|BEFORE_AND_AFTER|Devuelve los miembros descendientes de todos los niveles subordinados al nivel del miembro especificado. Incluye el miembro especificado, pero no incluye miembros del nivel especificado o a la distancia especificada.|  
|SELF_AND_AFTER|Devuelve los miembros descendientes desde el nivel especificado o a la distancia especificada y todos los niveles subordinados al nivel especificado o a la distancia especificada.|  
|SELF_AND_BEFORE|Devuelve los miembros descendientes desde el nivel especificado o a la distancia especificada y desde todos los niveles entre el miembro especificado y el nivel especificado, o a la distancia especificada, incluido el miembro especificado.|  
|SELF_BEFORE_AFTER|Devuelve los miembros descendientes de todos los niveles subordinados al nivel del miembro especificado e incluye éste.|  
|LEAVES|Devuelve los miembros descendientes hoja entre el miembro especificado y el nivel especificado, o a la distancia especificada.|  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el miembro especificado (Estados Unidos) y los miembros entre el miembro especificado (Estados Unidos) y los miembros del nivel anterior al nivel especificado (City). El ejemplo devuelve el propio miembro especificado (Estados Unidos) y los miembros del nivel State-Province (el nivel anterior al nivel City). Este ejemplo incluye argumentos comentados para permitir probar de manera sencilla otros argumentos para esta función.  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 En el ejemplo siguiente se devuelve el promedio diario de la `Measures.[Gross Profit Margin]` medida, calculado a lo largo de los días de cada mes del año fiscal 2003, del cubo **Adventure Works** . La función **Descendants** devuelve un conjunto de días determinado a partir del miembro actual de la `[Date].[Fiscal]` jerarquía.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 El ejemplo siguiente utiliza una expresión de nivel y devuelve Internet Sales Amount para cada State-Province de Australia, junto con el porcentaje del total de Internet Sales Amount para Australia para cada State-Province. En este ejemplo se usa la función Item para extraer la primera tupla (y solo) del conjunto devuelto por la función **antecesores** .  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
