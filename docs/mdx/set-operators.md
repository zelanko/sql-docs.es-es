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
ms.openlocfilehash: 6ad0b92a970c3618584365d9ad6e99420daef05d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037010"
---
# <a name="set-operators"></a>Operadores de conjuntos


  En las expresiones multidimensionales (MDX), los operadores de conjuntos ejecutan operaciones en miembros o conjuntos y devuelven un conjunto. Por lo general, los operadores de conjuntos se utilizan como alternativa a las distintas funciones de conjuntos en expresiones MDX.  
  
 MDX es compatible con los operadores de conjuntos que se indican en la siguiente tabla.  
  
|Operator|Descripción|  
|--------------|-----------------|  
|[-(Excepto)](../mdx/except-mdx-operator.md)|Devuelve la diferencia entre dos conjuntos y elimina los miembros duplicados.<br /><br /> Este operador es funcionalmente equivalente a la función [Except](../mdx/except-mdx-function.md) .|  
|[* (Crossjoin)](../mdx/crossjoin-mdx-operator-reference.md)|Devuelve el producto cruzado de dos conjuntos.<br /><br /> Este operador es funcionalmente equivalente a la función [Crossjoin](../mdx/crossjoin-mdx.md) .|  
|[: (Intervalo)](../mdx/range-mdx.md)|Devuelve un conjunto en su orden natural, con dos miembros especificados como extremos y todos los miembros entre ellos incluidos como miembros del conjunto.|  
|[+ (Unión)](../mdx/union-mdx-operator-reference.md)|Devuelve la unión de dos conjuntos y excluye los miembros duplicados.<br /><br /> Este operador es funcionalmente equivalente a la función [Union &#40;MDX&#41;](../mdx/union-mdx.md) .|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [Operadores &#40;sintaxis MDX&#41;](../mdx/operators-mdx-syntax.md)  
  
  
