---
description: NonEmptyCrossjoin (MDX)
title: NonEmptyCrossjoin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fafaad2f6fa0f46d826bf94b26ceb6fdbe9df55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471807"
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
  
## <a name="remarks"></a>Observaciones  
 La función **NonEmptyCrossjoin** devuelve el producto cruzado de dos o más conjuntos como un conjunto, excluyendo tuplas vacías o tuplas sin datos proporcionados por las tablas de hechos subyacentes. Debido a la forma en que funciona la función **NonEmptyCrossjoin** , se excluyen automáticamente todos los miembros calculados.  
  
 Si no se especifica *Count* , la función combina todos los conjuntos especificados y excluye los miembros vacíos del conjunto resultante. Si se especifica un número de conjuntos, la función realiza combinaciones cruzadas de los números de los conjuntos especificados, comenzando con el primer conjunto especificado. La función **NonEmptyCrossjoin** usa cualquier conjunto restante que se especifique en los conjuntos especificados subsiguientes, pero que no se hayan unido a la combinación para determinar qué miembros se consideran no vacíos en el conjunto combinado cruzado resultante. La función **NonEmptyCrossjoin** respeta el valor **NON_EMPTY_BEHAVIOR** de las medidas calculadas.  
  
> [!IMPORTANT]  
>  Esta función está desusada y no debería utilizarla; solo se conserva para mantener la compatibilidad con las versiones anteriores. En su lugar, debe utilizar la función [exists (MDX)](../mdx/exists-mdx.md) con el argumento de nombre del grupo de medida o la función [NonEmpty (MDX)](../mdx/nonempty-mdx.md) .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
