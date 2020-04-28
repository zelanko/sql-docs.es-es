---
title: Dividir (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6184aa9d932355cd935a9131848ec27895faea5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68049299"
---
# <a name="divide-mdx"></a>Divide (MDX)


  Realiza la división y devuelve un resultado alternativo o BLANK() al dividirlo entre 0.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *numera*  
 Dividendo o número que se va a dividir.  
  
 *denominador*  
 Divisor o número por el que se va a dividir.  
  
 *alternateresult*  
 (Opcional) El valor devuelto cuando la división entre cero da como resultado un error. Cuando no se proporciona, el valor predeterminado es BLANK().  
  
## <a name="remarks"></a>Observaciones  
 El resultado alternativo al dividir entre 0 debe ser una constante.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
