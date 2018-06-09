---
title: Dividir (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86b4d8c97996733396e3062e134b2e31d2819ec0
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739804"
---
# <a name="divide-mdx"></a>Divide (MDX)


  Realiza la división y devuelve un resultado alternativo o BLANK() al dividirlo entre 0.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Numerador*  
 Dividendo o número que se divide.  
  
 *denominador*  
 Divisor o número que se divide por.  
  
 *alternateresult*  
 (Opcional) El valor devuelto cuando la división entre cero da como resultado un error. Cuando no se proporciona, el valor predeterminado es BLANK().  
  
## <a name="remarks"></a>Notas  
 El resultado alternativo al dividir entre 0 debe ser una constante.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
