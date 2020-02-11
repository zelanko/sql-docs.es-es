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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
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
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un conjunto de tuplas vacías o un conjunto vacío, la función **AVG** devuelve un valor vacío.  
  
 La función **AVG** calcula el promedio de los valores no vacíos de las celdas del conjunto especificado calculando primero la suma de los valores de las celdas del conjunto especificado y, a continuación, dividiendo la suma calculada por el recuento de celdas no vacías del conjunto especificado.  
  
> [!NOTE]  
>  
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] omite los valores NULL al calcular el promedio de un conjunto de números.  
  
 Si no se especifica una expresión numérica específica (normalmente una medida), la función **AVG** calcula el promedio de cada medida en el contexto de la consulta actual. Si se proporciona una medida específica, la función **AVG** evalúa primero la medida en el conjunto y, a continuación, la función calcula el promedio basándose en la medida especificada.  
  
> [!NOTE]  
>  Al usar la función **CurrentMember** en una instrucción de miembro calculado, debe especificar una expresión numérica porque no existe ninguna medida predeterminada para la coordenada actual en dicho contexto de consulta.  
  
 Para forzar la inclusión de celdas vacías, la aplicación debe utilizar la función [CoalesceEmpty](../mdx/coalesceempty-mdx.md) o especificar una *Numeric_Expression* válida que proporcione un valor de cero (0) para los valores vacíos. Para obtener más información acerca de las celdas vacías, consulte la documentación de OLE DB.  
  
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
  
 En el ejemplo siguiente se devuelve el promedio diario `Measures.[Gross Profit Margin]` de la medida, calculado a lo largo de los días de cada mes del año fiscal 2003, del cubo **Adventure Works** . La función **AVG** calcula el promedio del conjunto de días contenidos en cada mes de la `[Ship Date].[Fiscal Time]` jerarquía. La primera versión del cálculo muestra el comportamiento predeterminado de Avg en la exclusión de los días que no registraron ventas por valor del promedio; la segunda versión muestra cómo se incluyen los días que no hubo ventas en el promedio.  
  
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
  
 En el ejemplo siguiente se devuelve el promedio diario `Measures.[Gross Profit Margin]` de la medida, calculado en los días de cada semestre del año fiscal 2003, del cubo **Adventure Works** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
