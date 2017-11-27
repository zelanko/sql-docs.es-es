---
title: Dividir (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2f05c20a10b72b3c919672fd528a4222c6d204d7
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="divide-mdx"></a>Divide (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Comentarios  
 El resultado alternativo al dividir entre 0 debe ser una constante.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

