---
description: MemberToStr (MDX)
title: MemberToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6217120c7e6d5ee55670be3d902a9ea99333273f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483808"
---
# <a name="membertostr-mdx"></a>MemberToStr (MDX)


  Devuelve una cadena con formato de expresiones multidimensionales (MDX) que corresponde a un miembro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MemberToStr(Member_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Esta función devuelve una cadena que contiene el nombre único de un miembro. Normalmente se usa para pasar el UniqueName de un miembro a una función externa.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve la cadena [Geography]. [Geografía]. [País]. & [Estados Unidos]:  
  
 `WITH MEMBER Measures.x AS MemberToStr`  
  
 `([Geography].[Geography].[Country].[United States])`  
  
 `SELECT Measures.x ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
