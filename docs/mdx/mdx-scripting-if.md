---
title: IF (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4975c455b942f053287b344a956a0083c8ca4e1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187504"
---
# <a name="mdx-scripting---if"></a>Scripting de MDX: IF


  Ejecuta una instrucción si la condición es true.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión MDX que se evalúa como un valor booleano que puede ser verdadero o falso.  
  
 *assignment*  
 Expresión MDX que asigna un valor a un subcubo o a una propiedad calculada.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la instrucción IF para el flujo de control, a diferencia del [IIf &#40;MDX&#41; ](../mdx/iif-mdx.md) función y el [instrucción CASE &#40;MDX&#41; ](../mdx/case-statement-mdx.md) que solo puede usarse para devolver valores u objetos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo, el ámbito se restringe al nivel Country de la jerarquía Customers Geography de la dimensión Customers. Si la medida actual es Internet Sales Amount, entonces Internet Sales Amount se establece en 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
