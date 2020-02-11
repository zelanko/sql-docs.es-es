---
title: VisualTotals (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a5becd3382f07a9adc89055a253235495a7e50a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125839"
---
# <a name="visualtotals-mdx"></a>VisualTotals (MDX)


  Devuelve un conjunto que se genera al calcular de forma dinámica el total de miembros secundarios de un conjunto especificado; opcionalmente puede utilizar un patrón para el nombre del miembro primario del conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Ajedrez*  
 Expresión de cadena válida para el miembro primario del conjunto que contiene un asterisco (*) como carácter de sustitución para el nombre primario.  
  
## <a name="remarks"></a>Observaciones  
 La expresión de conjunto especificada puede especificar un conjunto que contenga miembros en cualquier nivel de una única dimensión, generalmente miembros con una relación antecesor-descendiente. La función **VisualTotals** totaliza los valores de los miembros secundarios en el conjunto especificado y omite los miembros secundarios que no están en el conjunto al calcular los totales del resultado. Se suman visualmente los totales de los conjuntos ordenados jerárquicamente. Si el orden de los miembros de los conjuntos rompe la jerarquía, los resultados no son totales visuales. Por ejemplo, VisualTotals (USA, WA, CA, Seattle) no devuelve WA como Seattle. En cambio, devuelve los valores para WA, CA y Seattle y suma estos valores como el total visual para USA, contando dos veces las ventas para Seattle.  
  
> [!NOTE]  
>  Aplicar la función **VisualTotals** a los miembros de dimensión que no están relacionados con una medida o están bajo la granularidad del grupo de medida hará que los valores se reemplacen con NULL.  
  
 *Pattern*, que es opcional, especifica el formato de la etiqueta de totales. *Pattern* requiere un asterisco (*) como carácter de sustitución para el miembro primario y el resto del texto de la cadena aparece en el resultado concatenado con el nombre primario. Para mostrar un asterisco literal, use dos asteriscos (\*\*).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el total visual del tercer trimestre del año 2001, de acuerdo con el único descendiente especificado (el mes de julio).  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve el miembro [All] de la jerarquía de atributo Category de la dimensión Product, junto con dos de sus cuatro elementos secundarios. El total devuelto para el miembro [All] de la medida Internet Sales Amount es el total de los miembros Accessories y Clothing únicamente. Además, el argumento Pattern se utiliza para especificar la etiqueta para la columna [All Products].  
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
