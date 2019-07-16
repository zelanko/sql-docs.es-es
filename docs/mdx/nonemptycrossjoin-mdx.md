---
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2d152b51e0c1c996e0bb3309e554a70683937493
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088353"
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
  
 *Count*  
 Expresión numérica válida que especifica el número de conjuntos que serán devueltos.  
  
## <a name="remarks"></a>Comentarios  
 El **NonEmptyCrossjoin** función devuelve el producto cruzado de dos o más conjuntos como un conjunto, excluidas las tuplas vacías o sin datos proporcionados por las tablas de hechos subyacentes. Debido a cómo el **NonEmptyCrossjoin** función, todas se calculan automáticamente se excluyen los miembros.  
  
 Si *recuento* no se especifica, la función cross une todos los conjuntos especificados y excluye los miembros vacíos del conjunto resultante. Si se especifica un número de conjuntos, la función realiza combinaciones cruzadas de los números de los conjuntos especificados, comenzando con el primer conjunto especificado. El **NonEmptyCrossjoin** función utiliza los conjuntos restantes que se especifican en los conjuntos especificados subsiguientes, pero que no han cruzado unido para determinar qué miembros se consideran no vacíos en el conjunto combinado de forma cruzada resultante. El **NonEmptyCrossjoin** función respeta el **NON_EMPTY_BEHAVIOR** de medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta función está desusada y no debería utilizarla; solo se conserva para mantener la compatibilidad con las versiones anteriores. En su lugar, debe usar el [Exists (MDX)](../mdx/exists-mdx.md) canónica con el argumento de nombre de grupo de medida o la [NonEmpty (MDX)](../mdx/nonempty-mdx.md) función.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
