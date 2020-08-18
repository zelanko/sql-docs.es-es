---
description: Intersect (MDX)
title: Intersect (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9216b334caf67191e231c3ec0389da3fb7493b24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471847"
---
# <a name="intersect-mdx"></a>Intersect (MDX)


  Devuelve la intersección de dos conjuntos de entrada; conservando opcionalmente los duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Intersect(Set_Expression1 , Set_Expression2 [ , ALL ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Observaciones  
 La función **Intersect** devuelve la intersección de dos conjuntos. De manera predeterminada, la función quita los duplicados de ambos conjuntos antes de su intersección. Los dos conjuntos especificados deben tener la misma dimensionalidad.  
  
 La marca **All** opcional conserva los duplicados. Si se especifica **All** , la función **Intersect** forma una intersección con los elementos no duplicados como de costumbre y también intersecta cada duplicado del primer conjunto que tiene un duplicado coincidente en el segundo conjunto. Los dos conjuntos especificados deben tener la misma dimensionalidad.  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente devuelve los años 2003 y 2004, los dos miembros que aparecen en los dos conjuntos especificados:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001], [Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003]}`  
  
 `, {[Date].[Calendar Year].&[2002],[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 La consulta siguiente no se realiza correctamente porque los dos conjuntos especificados contienen miembros de jerarquías diferentes:  
  
 `SELECT`  
  
 `INTERSECT(`  
  
 `{[Date].[Calendar Year].&[2001]}`  
  
 `, {[Customer].[City].&[Abingdon]&[ENG]})`  
  
 `ON 0`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
