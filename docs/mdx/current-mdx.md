---
title: Actual (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 821d517419b90df44b7943a1e0edde12ef667b6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047123"
---
# <a name="current-mdx"></a>Current (MDX)


  Devuelve la tupla actual de un conjunto durante la iteración.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set_Expression.Current   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 En cada paso de una iteración, la tupla sobre la que se opera es la tupla actual. El **actual** función devuelve dicha tupla. Esta función solo es válida durante una iteración sobre un conjunto.  
  
 Incluyen funciones MDX que recorrer un conjunto el [generar](../mdx/generate-mdx.md) función.  
  
> [!NOTE]  
>  Esta función solo funciona con conjuntos con nombre, ya sea mediante un alias de conjunto o al definir un conjunto con nombre.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra cómo usar el **actual** función dentro de **generar**:  
  
 `WITH`  
  
 `//Creates a set of tuples consisting of all Calendar Years crossjoined with`  
  
 `//all Product Categories`  
  
 `SET MyTuples AS CROSSJOIN(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `//Iterates through each tuple in the set and returns the name of the Calendar`  
  
 `//Year in each tuple`  
  
 `MEMBER MEASURES.CURRENTDEMO AS`  
  
 `GENERATE(MyTuples, MyTuples.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
