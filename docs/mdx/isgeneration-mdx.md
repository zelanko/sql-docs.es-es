---
title: IsGeneration (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 401a11a10f190cda8efeaffa04e1025ef7f4e681
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105236"
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)


  Informa de si un miembro especificado es una generación especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Generation_Number*  
 Expresión numérica válida que especifica la generación con la que se evalúa el miembro especificado.  
  
## <a name="remarks"></a>Comentarios  
 El **IsGeneration** función devuelve **true** si el miembro especificado está en el número de generación especificado. En caso contrario, devuelve la función **false**. También, si el miembro especificado se evalúa como un miembro vacío, el **IsGeneration** función devuelve **false**.  
  
 Respecto a la indización de la generación, los miembros hoja son el índice 0 de la generación. En el índice de generación, los miembros no hoja se determinan obteniendo primero el índice de generación más alto de la unión de todos los miembros secundarios para el miembro especificado y agregando 1 a ese índice. Debido a la forma en que se determina la indización de la generación de los miembros no hoja, un miembro no hoja específico podría pertenecer a más de una generación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve TRUE si [Date].[Fiscal].CurrentMember es parte de la segunda generación:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
