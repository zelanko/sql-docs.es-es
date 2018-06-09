---
title: NonEmptyCrossjoin (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7da56ac658f57d6eb664762f9dd94351df39fe0f
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742654"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)


  Devuelve un conjunto que contiene el producto cruzado de uno o más conjuntos, excluidas las tuplas vacías y las que no tienen datos de la tabla de hechos asociada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recuento*  
 Expresión numérica válida que especifica el número de conjuntos que serán devueltos.  
  
## <a name="remarks"></a>Notas  
 El **NonEmptyCrossjoin** función devuelve el producto cruzado de dos o más conjuntos como un conjunto, excluidas las tuplas vacías o sin datos proporcionados por las tablas de hechos subyacente. Debido a cómo el **NonEmptyCrossjoin** función, todas las calculadas miembros se excluyen automáticamente.  
  
 Si *recuento* no se especifica, la función cross combina todos los conjuntos especificados y excluye los miembros vacíos del conjunto resultante. Si se especifica un número de conjuntos, la función realiza combinaciones cruzadas de los números de los conjuntos especificados, comenzando con el primer conjunto especificado. El **NonEmptyCrossjoin** función utiliza los conjuntos restantes que se especifican en los conjuntos especificados subsiguientes, pero que no han sido cruzado para determinar qué miembros se consideran no vacíos en el conjunto combinado de forma cruzada resultante. El **NonEmptyCrossjoin** función respeta el **NON_EMPTY_BEHAVIOR** configuración de las medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta función está desusada y no debería utilizarla; solo se conserva para mantener la compatibilidad con las versiones anteriores. En su lugar, debe utilizar el [Exists (MDX)](../mdx/exists-mdx.md) función con el argumento de nombre de grupo de medida o la [NonEmpty (MDX)](../mdx/nonempty-mdx.md) (función).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
