---
title: Especificar el contenido de un eje segmentador (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slicer axis
- filtering data [MDX]
ms.assetid: c56b0a70-cdec-427f-990e-425290344e7d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12e2d2f543694a1da418f5e8eb4b900eaa123d97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074059"
---
# <a name="specifying-the-contents-of-a-slicer-axis-mdx"></a>Especificar el contenido de un eje de división en sectores (MDX)
  El eje segmentador filtra los datos devueltos por la instrucción SELECT de Expresiones multidimensionales (MDX) y restringe los datos devueltos de forma que solamente se devuelvan los datos de intersección entre los miembros especificados. Puede considerarse como eje adicional no visible en una consulta. El eje segmentador se define en la cláusula WHERE de la instrucción SELECT de MDX.  
  
## <a name="slicer-axis-syntax"></a>Sintaxis del eje segmentador  
 Para especificar explícitamente un eje segmentador, debe utilizar `<SELECT slicer axis clause>` en MDX, según se describe en la siguiente sintaxis:  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 En la sintaxis del eje segmentador que se muestra, `Set_Expression` puede tomar una expresión de tupla, que se trata como un conjunto en cuanto a la evaluación de la cláusula, o como una expresión de conjunto. Si se especifica una expresión de conjunto, MDX intentará evaluar el conjunto, sumando las celdas de resultado en cada tupla del conjunto. En otras palabras, MDX intentará utilizar la función [Aggregate](/sql/mdx/aggregate-mdx) en el conjunto, agregando cada medida por su función de agregación asociada. Asimismo, si la expresión de conjunto no puede expresarse como un cruce de miembros de la jerarquía de atributos, MDX trata las celdas que quedan fuera de la expresión de conjunto para el segmentador como valores nulos (NULL) para fines de evaluación.  
  
> [!IMPORTANT]  
>  A diferencia de la cláusula WHERE de SQL, la cláusula WHERE de una instrucción MDX SELECT no filtra nunca directamente lo que se devuelve en el eje de filas de una consulta. Para filtrar qué aparece en el eje de filas o columnas de una consulta, puede utilizar una variedad de funciones MDX, como FILTER, NON EMPTY y TOPCOUNT.  
  
### <a name="implicit-slicer-axis"></a>Eje segmentador implícito  
 Si un miembro de una jerarquía del cubo no está explícitamente incluido en un eje de consulta, el miembro predeterminado de esa jerarquía se incluye implícitamente en el eje segmentador. Para más información sobre los miembros predeterminados, vea [Definir un miembro predeterminado](../attribute-properties-define-a-default-member.md).  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente no incluye la cláusula WHERE y devuelve el valor de la medida Internet Sales Amount para todos los años naturales:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 Agregar una cláusula WHERE, como sigue:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 no cambia lo que se devuelve en las filas o columnas de la consulta; cambia los valores devueltos para cada celda. En este ejemplo, se crean sectores de la consulta para que devuelva el valor de Internet Sales Amount para todos los años naturales, pero solo para los clientes que viven en los Estados Unidos. Varios miembros de diferentes jerarquías pueden agregarse a la cláusula WHERE. La consulta siguiente muestra el valor de Internet Sales Amount para todos los años naturales para los clientes que viven en Estados Unidos y que compraron productos de la categoría bicicletas:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 Si desea utilizar varios miembros de la misma jerarquía, debe incluir un conjunto en la cláusula WHERE. Por ejemplo, la siguiente consulta muestra el valor de Internet Sales Amount para todos los años naturales para los clientes que compraron productos de la categoría bicicletas y viven en Estados Unidos o Reino Unido:  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 Como se mencionó anteriormente, con un conjunto en la cláusula WHERE agregará implícitamente los valores de todos los miembros del conjunto. En este caso, la consulta muestra los valores agregados para Estados Unidos y Reino Unido en cada celda.  
  
  
