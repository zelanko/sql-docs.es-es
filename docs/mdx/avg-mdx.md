---
title: AVG (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa8817e35a589def4631bd455637d05fc62d3a0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017012"
---
# <a name="avg-mdx"></a>Avg (MDX)


  Evalúa un conjunto y devuelve el promedio de los valores no vacíos de las celdas del conjunto promediados con las medidas del conjunto o una medida especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX válida que devuelve un conjunto  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica un conjunto de tuplas vacías o un conjunto vacío, el **Avg** función devuelve un valor vacío.  
  
 El **Avg** función calcula el promedio de los valores no vacíos de las celdas del conjunto especificado al calcular la suma de valores en las celdas del conjunto especificado en primer lugar y, a continuación, dividir la suma calculada por el recuento de celdas no vacías el conjunto especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] omite los valores NULL al calcular el promedio de un conjunto de números.  
  
 Si no se especifica una expresión numérica concreta (normalmente una medida), el **Avg** función calcula el promedio de cada medida dentro del contexto de consulta actual. Si se proporciona una medida específica, la **Avg** función primero evalúa la medida en el conjunto y, a continuación, la función calcula el promedio basado en la medida especificada.  
  
> [!NOTE]  
>  Cuando se usa el **CurrentMember** función en una declaración de miembro calculado, debe especificar una expresión numérica, porque no existe ninguna medida predeterminada para la coordenada actual en este contexto de consulta.  
  
 Para forzar la inclusión de las celdas vacías, la aplicación debe utilizar el [CoalesceEmpty](../mdx/coalesceempty-mdx.md) función o especifique una válida *Numeric_Expression* que proporcione un valor de cero (0) para los valores vacíos. Para obtener más información acerca de las celdas vacías, consulte la documentación de OLE DB.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo devuelve el promedio de una medida sobre un conjunto especificado. Tenga en cuenta que la medida especificada puede ser la medida predeterminada para los miembros del conjunto especificado o una medida especificada.  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 El ejemplo siguiente devuelve el promedio diario de la `Measures.[Gross Profit Margin]` medida calculada en los días de cada mes del año fiscal 2003, desde el **Adventure Works** cubo. El **Avg** función calcula el promedio del conjunto de días que se encuentran en cada mes de la `[Ship Date].[Fiscal Time]` jerarquía. La primera versión del cálculo muestra el comportamiento predeterminado de Avg en la exclusión de los días que no registraron ventas por valor del promedio; la segunda versión muestra cómo se incluyen los días que no hubo ventas en el promedio.  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 El ejemplo siguiente devuelve el promedio diario de la `Measures.[Gross Profit Margin]` medida calculada en los días de cada semestre del año fiscal 2003, desde el **Adventure Works** cubo.  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
