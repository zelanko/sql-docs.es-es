---
title: IF (instrucción, MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7426c609de80ab249cd71e4364979ff07165598
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579867"
---
# <a name="mdx-scripting---if"></a>Scripting de MDX - IF
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ejecuta una instrucción si la condición es true.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IF expression THEN assignment END IF  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión MDX que se evalúa como un valor booleano que puede ser verdadero o falso.  
  
 *Asignación*  
 Expresión MDX que asigna un valor a un subcubo o a una propiedad calculada.  
  
## <a name="remarks"></a>Notas  
 Utilice la instrucción IF para el flujo de control, que es diferente a la [IIf &#40;MDX&#41; ](../mdx/iif-mdx.md) función y la [instrucción CASE &#40;MDX&#41; ](../mdx/case-statement-mdx.md) que solo se puede utilizar para devolver valores u objetos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo, el ámbito se restringe al nivel Country de la jerarquía Customers Geography de la dimensión Customers. Si la medida actual es Internet Sales Amount, entonces Internet Sales Amount se establece en 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
