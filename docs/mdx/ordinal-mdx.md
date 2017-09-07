---
title: Ordinal (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Ordinal
dev_langs:
- kbMDX
helpviewer_keywords:
- Ordinal function
ms.assetid: 9d416c39-da4a-4f0d-8d85-a76af5df0a87
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b848698799bc0c620d9592e90f508f01ac279f6f
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor ordinal (con base cero) asociado a un nivel.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Comentarios  
 El **Ordinal** función se utiliza habitualmente junto con el **IIF** y **CurrentMember** funciones para mostrar condicionalmente distintos valores en diferentes niveles de jerarquía, basándose en la posición ordinal de cada celda específica en el resultado de la consulta. Por ejemplo, puede usar el **Ordinal** función para realizar cálculos en ciertos niveles y mostrará el valor predeterminado "N/A" en otros niveles.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el número ordinal del nivel Calendar Quarter de la jerarquía Calendar.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  

