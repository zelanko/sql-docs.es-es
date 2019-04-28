---
title: FirstSibling (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1cb097e89a36eaa4d7ef68eca3b88aa6ca03d49a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690415"
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)


  Devuelve el primer elemento secundario del elemento primario de un miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.FirstSibling   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
### <a name="example"></a>Ejemplo  
 La consulta siguiente devuelve el primer miembro del mismo nivel que el año fiscal 2003 de la jerarquía Fiscal, que es el año fiscal 2002.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstSibling ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
