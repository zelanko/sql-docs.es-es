---
title: Elementos de sintaxis de MDX (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 263238a0d8430928fad99042dfa0ffd06921a33b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893318"
---
# <a name="mdx-syntax-elements-mdx"></a>Elementos de la sintaxis de MDX (MDX)


  Las expresiones multidimensionales (MDX) tienen varios elementos utilizados por la mayor parte de las instrucciones, o bien que influyen en las mismas:  
  
|Término|Definición|  
|----------|----------------|  
|[Identificadores](../mdx/identifiers-mdx.md)|Los identificadores son los nombres de objetos, como cubos, dimensiones, miembros y medidas.|  
|**Tipo de datos**|Definen los tipos de datos que contienen las celdas, las propiedades de miembro y las propiedades de celda. MDX solo admite el tipo de datos OLE VARIANT. Para obtener más información acerca de la coerción, la conversión y la manipulación del tipo de datos VARIANT, vea el tema sobre VARIANT y VARIANTARG en la documentación de Platform SDK.|  
|[Expresiones &#40;&#41;MDX](../mdx/expressions-mdx.md)|Las expresiones son unidades de sintaxis que Analysis Services pueden resolver en objetos o valores únicos (escalares). Las expresiones incluyen funciones que devuelven un solo valor, una expresión de conjunto, etc.|  
|[Operadores](../mdx/operators-mdx-syntax.md)|Los operadores son elementos de sintaxis que funcionan con una o más expresiones MDX simples para crear expresiones MDX más complejas.|  
|[Functions](../mdx/functions-mdx-syntax.md)|Las funciones son elementos de sintaxis que toman cero, uno o más valores de entrada y devuelven un valor escalar o un objeto. Algunos ejemplos son la función [SUM](../mdx/sum-mdx.md) para agregar varios valores, la función [Members](../mdx/members-set-mdx.md) para devolver un conjunto de miembros de una dimensión o un nivel, etc.|  
|[Comentarios](../mdx/comments-mdx-syntax.md)|Los comentarios son fragmentos de texto insertados en instrucciones o scripts MDX para explicar el objetivo de la instrucción. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]no ejecuta Comentarios.|  
|[Palabras clave reservadas](../mdx/reserved-keywords-mdx-syntax.md)|Las palabras clave reservadas son palabras que se han reservado para usarse con MDX y que no deberían utilizarse para nombres de objeto que se empleen en instrucciones MDX.|  
|[Miembros, tuplas y conjuntos (MDX)](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)|Los miembros, las tuplas y los conjuntos son conceptos básicos de los datos multidimensionales que es imprescindible comprender antes de crear una consulta MDX.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de expresiones multidimensionales &#40;MDX&#41;](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
