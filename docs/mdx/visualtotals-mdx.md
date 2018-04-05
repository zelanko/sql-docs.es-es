---
title: VisualTotals (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- VisualTotals
dev_langs:
- kbMDX
helpviewer_keywords:
- VisualTotals function
ms.assetid: 8ec529c2-729a-4a5b-892e-750849ab4013
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3270bf4f47b4ceafe6d5e1479e870d0492c7c37b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="visualtotals-mdx"></a>VisualTotals (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un conjunto que se genera al calcular de forma dinámica el total de miembros secundarios de un conjunto especificado; opcionalmente puede utilizar un patrón para el nombre del miembro primario del conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Patrón*  
 Expresión de cadena válida para el miembro primario del conjunto que contiene un asterisco (*) como carácter de sustitución para el nombre primario.  
  
## <a name="remarks"></a>Comentarios  
 La expresión de conjunto especificada puede especificar un conjunto que contenga miembros en cualquier nivel de una única dimensión, generalmente miembros con una relación antecesor-descendiente. El **VisualTotals** función suma los valores de los miembros secundarios en el conjunto especificado y omite los miembros secundarios que no están en el conjunto de calcular los resultados totales. Se suman visualmente los totales de los conjuntos ordenados jerárquicamente. Si el orden de los miembros de los conjuntos rompe la jerarquía, los resultados no son totales visuales. Por ejemplo, VisualTotals (USA, WA, CA, Seattle) no devuelve WA como Seattle. En cambio, devuelve los valores para WA, CA y Seattle y suma estos valores como el total visual para USA, contando dos veces las ventas para Seattle.  
  
> [!NOTE]  
>  Aplicar el **VisualTotals** función a los miembros de dimensión que no están relacionadas con una medida o están bajo la granularidad del grupo de medida hará que los valores se sustituyan por un valor nulo.  
  
 *Patrón de*, que es opcional, especifica el formato de la etiqueta de totales. *Patrón de* exige un asterisco (*) como carácter de sustitución para el miembro primario y el resto del texto de la cadena aparece en el resultado concatenado con el nombre primario. Para mostrar un asterisco literal, utilice dos asteriscos (\*\*).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
