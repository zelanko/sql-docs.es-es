---
description: IF (instrucción, MDX)
title: IF (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 62b5a2e7d2ae04b7cd11bb08a3a65ddad903b6cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429737"
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
  
 *asignación*  
 Expresión MDX que asigna un valor a un subcubo o a una propiedad calculada.  
  
## <a name="remarks"></a>Observaciones  
 Use la instrucción IF para el flujo de control, que es a diferencia de la función [IIf &#40;mdx&#41;](../mdx/iif-mdx.md) y la [instrucción CASE &#40;MDX&#41;](../mdx/case-statement-mdx.md) que solo se puede usar para devolver valores u objetos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo, el ámbito se restringe al nivel Country de la jerarquía Customers Geography de la dimensión Customers. Si la medida actual es Internet Sales Amount, entonces Internet Sales Amount se establece en 10:  
  
 `SCOPE ([Customer].[Customer Geography].[Country].MEMBERS);`  
  
 `IF Measures.CurrentMember IS [Measures].[Internet Sales Amount] THEN this = 10 END IF;`  
  
 `END SCOPE`;  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
