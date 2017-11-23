---
title: "IF (instrucción, MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: statements [MDX], IF
ms.assetid: 8830cce5-9e06-4f89-a555-295bb0d0a8a1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c5eaeffbc4ede2bedf0d85d8ef0ec4b40fb1993b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-scripting---if"></a>Scripting de MDX - IF
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ejecuta una instrucción si la condición es true.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión MDX que se evalúa como un valor booleano que puede ser verdadero o falso.  
  
 *asignación*  
 Expresión MDX que asigna un valor a un subcubo o a una propiedad calculada.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la instrucción IF para el flujo de control, que es diferente a la [IIf &#40; MDX &#41; ](../mdx/iif-mdx.md) función y el [instrucción CASE &#40; MDX &#41; ](../mdx/case-statement-mdx.md) que solo se puede utilizar para devolver valores u objetos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo, el ámbito se restringe al nivel Country de la jerarquía Customers Geography de la dimensión Customers. Si la medida actual es Internet Sales Amount, entonces Internet Sales Amount se establece en 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
