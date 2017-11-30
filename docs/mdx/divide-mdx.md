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
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ec7d1cf6bf0cd7b702d633c4022230f93a686b53
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
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
  
  
