---
description: Current (MDX)
title: Actual (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 105bb306cb84f151024a288f5aa15eb09ddbf5c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387551"
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
  
## <a name="remarks"></a>Observaciones  
 En cada paso de una iteración, la tupla sobre la que se opera es la tupla actual. La función **actual** devuelve esa tupla. Esta función solo es válida durante una iteración sobre un conjunto.  
  
 Las funciones MDX que recorren en iteración un conjunto incluyen la función [Generate](../mdx/generate-mdx.md) .  
  
> [!NOTE]  
>  Esta función solo funciona con conjuntos con nombre, ya sea mediante un alias de conjunto o al definir un conjunto con nombre.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo usar la función **actual** dentro de **Generate**:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
