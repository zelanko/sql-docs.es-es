---
title: NOT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b70068562ff24e8a1619b85fe091ab3e17da173
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278494"
---
# <a name="not-mdx"></a>NOT (MDX)


  Realiza una negación lógica de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **false** si el argumento se evalúa como **true**; en caso contrario, **true**.  
  
## <a name="remarks"></a>Comentarios  
 El **no** operador trata la expresión como un valor booleano (cero, 0, como **false**; en caso contrario, **true**) antes de que el operador realice la negación lógica. La tabla siguiente se muestra cómo el **no** operador realiza la negación lógica.  
  
|*Expression1*|Valor devuelto|  
|-------------------|------------------|  
|**true**|**False**|  
|**False**|**true**|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
