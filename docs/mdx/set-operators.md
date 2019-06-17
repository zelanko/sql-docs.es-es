---
title: Operadores de conjuntos | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df58b5c7f6da05700f00b4ec5fd46b81926dd3bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150170"
---
# <a name="set-operators"></a>Operadores de conjuntos


  En las expresiones multidimensionales (MDX), los operadores de conjuntos ejecutan operaciones en miembros o conjuntos y devuelven un conjunto. Por lo general, los operadores de conjuntos se utilizan como alternativa a las distintas funciones de conjuntos en expresiones MDX.  
  
 MDX es compatible con los operadores de conjuntos que se indican en la siguiente tabla.  
  
|Operador|Descripción|  
|--------------|-----------------|  
|[- (Excepto)](../mdx/except-mdx-operator.md)|Devuelve la diferencia entre dos conjuntos y elimina los miembros duplicados.<br /><br /> Este operador es funcionalmente equivalente a la [excepto](../mdx/except-mdx-function.md) función.|  
|[* (Combinaciones cruzadas)](../mdx/crossjoin-mdx-operator-reference.md)|Devuelve el producto cruzado de dos conjuntos.<br /><br /> Este operador es funcionalmente equivalente a la [Crossjoin](../mdx/crossjoin-mdx.md) función.|  
|[: (Range)](../mdx/range-mdx.md)|Devuelve un conjunto en su orden natural, con dos miembros especificados como extremos y todos los miembros entre ellos incluidos como miembros del conjunto.|  
|[+ (Unión)](../mdx/union-mdx-operator-reference.md)|Devuelve la unión de dos conjuntos y excluye los miembros duplicados.<br /><br /> Este operador es funcionalmente equivalente a la [unión &#40;MDX&#41; ](../mdx/union-mdx.md) función.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis de MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
