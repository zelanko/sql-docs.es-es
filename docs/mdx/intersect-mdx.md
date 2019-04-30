---
title: Intersect (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b24049cb81982075fa9234c6fa792db273d404db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224873"
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
  
## <a name="remarks"></a>Comentarios  
 El **Intersect** función devuelve la intersección de dos conjuntos. De manera predeterminada, la función quita los duplicados de ambos conjuntos antes de su intersección. Los dos conjuntos especificados deben tener la misma dimensionalidad.  
  
 El elemento opcional **todas** marca conserva los duplicados. Si **todas** se especifica, el **Intersect** función intersecta intersecta elementos como de costumbre y también intersecta cada duplicado del primer conjunto que tenga un duplicado coincidente en el segundo conjunto. Los dos conjuntos especificados deben tener la misma dimensionalidad.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
