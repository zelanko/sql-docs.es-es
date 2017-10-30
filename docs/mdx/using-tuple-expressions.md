---
title: Usar expresiones de tupla | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- single-member tuples [MDX]
- expressions [MDX], tuples
- one-member tuples
- tuples
- implicit tuples
ms.assetid: 0b802b76-9123-405e-ae43-d438754724ba
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f0d24279e896bc71faef81c5901d6d52069b717c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="using-tuple-expressions"></a>Usar expresiones de tupla
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Una tupla se compone de un miembro de cada una de las dimensiones incluidas en un cubo. Por lo tanto, una tupla identifica de forma única una sola celda de un cubo.  
  
> [!NOTE]  
>  Una tupla que haga referencia a uno o más miembros no válidos se denomina tupla vacía.  
  
 La expresión completa de un identificador de tupla está formada por uno o más miembros especificados de forma explícita entre paréntesis:  
  
 (*Expresión_miembro* [,*expresión_miembro* ...])  
  
 Una tupla puede especificarse de forma completa y puede incluir miembros implícitos o un solo miembro.  
  
## <a name="tuples-and-implicit-members"></a>Tuplas y miembros implícitos  
 Una tupla que especifique de forma explícita un solo miembro de cada una de las dimensiones de un cubo se denomina tupla completa. Sin embargo, no es necesario que las tuplas tengan un nombre completo.  
  
 Las dimensiones a las que no se haga referencia explícita en una tupla se consideran dimensiones con referencia implícita. El miembro de la dimensión a la que se hace referencia de forma implícita depende de la estructura de la dimensión y de las relaciones de atributo definidas en su interior. Si hay una referencia explícita a una jerarquía en la misma dimensión que la jerarquía a la que se hace referencia de forma implícita y hay una relación directa o indirecta definida entre la jerarquía a la que se hace referencia de forma explícita y la jerarquía a la que se hace referencia de forma implícita, la tupla se comporta como si contuviese el miembro en la jerarquía a la que se hace referencia de forma implícita, que coexiste con el miembro en la jerarquía a la que se hace referencia de forma explícita. Por ejemplo, si un cubo contiene una dimensión Cliente con los atributos Ciudad y País y hay una relación definida entre estos dos atributos para que una Ciudad tenga un País y un País puede contener muchas Ciudades, al incluir explícitamente la Ciudad 'Londres' en la tupla, hará referencia implícitamente al País 'Reino Unido'. Sin embargo, si no se define ninguna relación de atributo, la dirección de la relación es la contraria (por ejemplo, aunque Ciudad podría tener una relación con País, no es posible determinar la Ciudad en la que alguien vive si solo se conoce el País) o no hay ninguna relación directa entre los dos atributos definidos (podría haber una relación definida de Cliente a Ciudad y de Cliente a País, pero no hay ninguna relación definida entre Ciudad y País), se aplican las reglas siguientes:  
  
-   Si la jerarquía a la que se hace referencia implícitamente tiene un miembro predeterminado, éste se agrega a la tupla.  
  
-   Si la jerarquía con referencia implícita no tiene ningún miembro predeterminado, el **(All)** se utiliza el miembro de la jerarquía de manera predeterminada.  
  
-   Cuando la jerarquía con referencia implícita no tiene ningún miembro predeterminado, se utiliza el primer miembro del nivel superior de la jerarquía.  
  
## <a name="one-member-tuples"></a>Tuplas de un miembro  
 Si la expresión de tupla tiene un solo miembro, MDX convierte el miembro en una tupla de un solo miembro a fin de evaluar la expresión. Es decir, funcionalmente es lo mismo utilizar la expresión de miembro `[Measures].[TestMeasure]` en lugar de la expresión de tupla que utilizar la expresión de tupla `( [Measures].[TestMeasure] ).`.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; MDX &#41;](../mdx/expressions-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

