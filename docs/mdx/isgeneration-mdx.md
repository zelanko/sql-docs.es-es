---
title: IsGeneration (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ISGENERATION
dev_langs: kbMDX
helpviewer_keywords: IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9d0b8adb889a555155d8030413b855c5663a776e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  Informa de si un miembro especificado es una generación especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Generation_Number*  
 Expresión numérica válida que especifica la generación con la que se evalúa el miembro especificado.  
  
## <a name="remarks"></a>Comentarios  
 El **IsGeneration** función devuelve **true** si el miembro especificado está en el número de generación especificado. En caso contrario, la función devuelve **false**. También, si el miembro especificado se evalúa como un miembro vacío, la **IsGeneration** función devuelve **false**.  
  
 Respecto a la indización de la generación, los miembros hoja son el índice 0 de la generación. En el índice de generación, los miembros no hoja se determinan obteniendo primero el índice de generación más alto de la unión de todos los miembros secundarios para el miembro especificado y agregando 1 a ese índice. Debido a la forma en que se determina la indización de la generación de los miembros no hoja, un miembro no hoja específico podría pertenecer a más de una generación.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve TRUE si [Date].[Fiscal].CurrentMember es parte de la segunda generación:  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
