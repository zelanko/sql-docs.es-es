---
title: Trabajar con miembros, tuplas y conjuntos (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MDX [Analysis Services], tuples
- member keys [MDX]
- MDX [Analysis Services], sets
- calculated members [MDX]
- members [MDX]
- Multidimensional Expressions [Analysis Services], members
- named sets [MDX]
- Multidimensional Expressions [Analysis Services], tuples
- member functions [MDX]
- sets [MDX]
- MDX [Analysis Services], members
- member names [MDX]
- Multidimensional Expressions [Analysis Services], sets
- tuple functions
- tuples
- set functions [MDX]
ms.assetid: b6ec2439-caef-46d3-9fd7-5f4526cee334
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fbd4fa53eb870bc8422dcb80fe019083e773e638
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153266"
---
# <a name="working-with-members-tuples-and-sets-mdx"></a>Trabajar con miembros, tuplas y conjuntos (MDX)
  MDX proporciona varias funciones que devuelven uno o más miembros, tuplas o conjuntos; o que actúan sobre un miembro, tupla o conjunto.  
  
## <a name="member-functions"></a>Funciones de miembro  
 MDX proporciona varias funciones para recuperar miembros de otras entidades MDX, por ejemplo desde dimensiones, niveles, conjuntos o tuplas. Por ejemplo, [FirstChild](/sql/mdx/firstchild-mdx) es una función que actúa sobre un miembro y devuelve un miembro.  
  
 Para obtener el primer miembro secundario de la dimensión Time, se debe indicar explícitamente el miembro, como en el siguiente ejemplo.  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 También puede usar el `FirstChild` función para devolver el mismo miembro, como se muestra en el ejemplo siguiente.  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 Para obtener más información sobre las funciones de miembro de MDX, vea [MDX Function Reference &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="tuple-functions"></a>funciones de tupla  
 MDX proporciona varias funciones que devuelven tuplas y que se pueden utilizar en cualquier ubicación en la que se acepte una tupla. Por ejemplo, la función [Item &#40;Tuple&#41; &#40;MDX&#41;](/sql/mdx/item-tuple-mdx) puede usarse para extraer la primera tupla de un conjunto, lo que resulta muy útil cuando se sabe que un conjunto está compuesto por una sola tupla y se quiere proporcionar esa tupla a una función que requiere una.  
  
 El ejemplo siguiente devuelve la primera tupla desde el conjunto de tuplas en el eje de columna.  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 Para obtener más información sobre las funciones de tupla, vea [MDX Function Reference &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="set-functions"></a>Funciones de conjunto  
 MDX proporciona varias funciones que devuelven conjuntos. Escribir tuplas explícitamente y encerrarlas entre llaves no es la única manera de recuperar un conjunto. Para obtener más información sobre la función de miembros para devolver un conjunto, vea [Key Concepts in MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md). Hay muchas más funciones de conjunto.  
  
 El operador dos puntos (:) permite utilizar el orden natural de los miembros para crear un conjunto. Por ejemplo, el conjunto que se muestra en el siguiente ejemplo incluye tuplas del primer al cuarto trimestre del año 2002.  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 Si no utiliza el operador dos puntos para crear el conjunto, puede crear el mismo conjunto de miembros al especificar las tuplas en el siguiente ejemplo:  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 El operador dos puntos es una función inclusiva. Los miembros ubicados a ambos lados del operador dos puntos se incluyen en el conjunto resultante.  
  
 Para obtener más información sobre las funciones de conjuntos, vea [MDX Function Reference &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="array-functions"></a>Funciones de matriz  
 Una función de matriz actúa sobre un conjunto y devuelve una matriz. Para obtener más información sobre las funciones de matriz, vea [MDX Function Reference &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="hierarchy-functions"></a>Funciones de jerarquía  
 Una función de jerarquía devuelve una jerarquía al actuar sobre un miembro, un nivel, una jerarquía o una cadena. Para obtener más información sobre las funciones de jerarquía, vea [MDX Function Reference &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="level-functions"></a>Funciones de nivel  
 Una función de nivel devuelve un nivel al actuar sobre un miembro, un nivel o una cadena. Para obtener más información sobre las funciones de nivel, vea [MDX Function Reference &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="logical-functions"></a>Funciones lógicas  
 Una función lógica actúa sobre una expresión MDX para devolver información acerca de las tuplas, miembros o conjuntos de la expresión. Por ejemplo, la función [IsEmpty &#40;MDX&#41;](/sql/mdx/isempty-mdx) evalúa si una expresión ha devuelto un valor de celda vacía. Para obtener más información sobre las funciones lógicas, vea [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="numeric-functions"></a>Funciones numéricas  
 Una función numérica actúa sobre una expresión MDX para devolver un valor escalar. Por ejemplo, la función [Aggregate &#40;MDX&#41;](/sql/mdx/aggregate-mdx) devuelve un valor escalar que se calcula al agregar medidas sobre las tuplas de un conjunto especificado. Para obtener más información sobre las funciones numéricas, vea [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="string-functions"></a>Funciones de cadena  
 Una función de cadena actúa sobre una expresión MDX para devolver una cadena. Por ejemplo, la función [UniqueName &#40;MDX&#41;](/sql/mdx/uniquename-mdx) devuelve un valor de cadena que contiene el nombre único de una dimensión, jerarquía, nivel o miembro. Para obtener más información sobre las funciones de cadena, vea [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx).  
  
## <a name="see-also"></a>Vea también  
 [Conceptos clave para MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Aspectos básicos de consultas MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
