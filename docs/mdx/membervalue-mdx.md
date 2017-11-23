---
title: MemberValue (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: MEMBERVALUE
dev_langs: kbMDX
helpviewer_keywords: MemberValue function
ms.assetid: f9b2af16-2b81-48e4-ae81-99f64e4bbc98
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2d6a74903eb98002864e8d3ae5a68e5af4f07112
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor de un miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX (Expresiones multidimensionales) válida que se evalúa en un miembro.  
  
## <a name="return-value"></a>Valor devuelto  
 El valor de miembro devuelto incluye la información que se indica a continuación, en el orden en el que aparece en el valor devuelto:  
  
-   El enlace de valor, si se ha definido.  
  
-   La clave con el tipo de datos original si no hay enlace de nombres o si la clave y el título están enlazados a la misma columna.  
  
-   El título del miembro.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el enlace de valor, la clave de miembro y el título de la primera fecha de la dimensión Date del cubo Adventure Works.  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
