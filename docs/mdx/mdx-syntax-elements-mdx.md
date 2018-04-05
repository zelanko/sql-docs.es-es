---
title: Elementos de sintaxis MDX (MDX) | Documentos de Microsoft
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
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], syntax
- MDX [Analysis Services], syntax
ms.assetid: f4c16e1a-cf1a-4be0-839a-db018430ff14
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 7ed42f669cd9e78faa738e876b1872c83c98a790
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-syntax-elements-mdx"></a>Elementos de la sintaxis de MDX (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Las expresiones multidimensionales (MDX) tienen varios elementos utilizados por la mayor parte de las instrucciones, o bien que influyen en las mismas:  
  
|Término|Definición|  
|----------|----------------|  
|[Identificadores](../mdx/identifiers-mdx.md)|Los identificadores son los nombres de objetos, como cubos, dimensiones, miembros y medidas.|  
|**Tipos de datos**|Definen los tipos de datos que contienen las celdas, las propiedades de miembro y las propiedades de celda. MDX solo admite el tipo de datos OLE VARIANT. Para obtener más información acerca de la coerción, la conversión y la manipulación del tipo de datos VARIANT, vea el tema sobre VARIANT y VARIANTARG en la documentación de Platform SDK.|  
|[Expresiones &#40; MDX &#41;](../mdx/expressions-mdx.md)|Las expresiones son unidades de sintaxis que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede resolver en valores (escalares) u objetos. Las expresiones incluyen funciones que devuelven un solo valor, una expresión de conjunto, etc.|  
|[Operadores](../mdx/operators-mdx-syntax.md)|Los operadores son elementos de sintaxis que funcionan con una o más expresiones MDX simples para crear expresiones MDX más complejas.|  
|[Funciones](../mdx/functions-mdx-syntax.md)|Las funciones son elementos de sintaxis que toman cero, uno o más valores de entrada y devuelven un valor escalar o un objeto. Algunos ejemplos son la [suma](../mdx/sum-mdx.md) función para agregar varios valores, el [miembros](../mdx/members-set-mdx.md) función para devolver un conjunto de miembros de una dimensión o un nivel y así sucesivamente.|  
|[Comentarios](../mdx/comments-mdx-syntax.md)|Los comentarios son fragmentos de texto insertados en instrucciones o scripts MDX para explicar el objetivo de la instrucción. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]no ejecuta los comentarios.|  
|[Palabras clave reservadas](../mdx/reserved-keywords-mdx-syntax.md)|Las palabras clave reservadas son palabras que se han reservado para usarse con MDX y que no deberían utilizarse para nombres de objeto que se empleen en instrucciones MDX.|  
|[Miembros, tuplas y conjuntos](../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)|Los miembros, las tuplas y los conjuntos son conceptos básicos de los datos multidimensionales que es imprescindible comprender antes de crear una consulta MDX.|  
  
## <a name="see-also"></a>Vea también  
 [Expresiones multidimensionales &#40; MDX &#41; Referencia](../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
