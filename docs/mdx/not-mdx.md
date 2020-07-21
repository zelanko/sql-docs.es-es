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
ms.openlocfilehash: 4031b887eb0a42580d6ae8debf6c9177ff67efc3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088235"
---
# <a name="not-mdx"></a>NOT (MDX)


  Realiza una negación lógica de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Argumento*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor booleano que devuelve **false** si el argumento se evalúa como **true**; en caso contrario, **true**.  
  
## <a name="remarks"></a>Observaciones  
 El operador **Not** trata la expresión como un valor booleano (cero, 0, como **false**; de lo contrario, **true**) antes de que el operador realice la negación lógica. En la tabla siguiente se muestra cómo el operador **Not** realiza la negación lógica.  
  
|*Argumento*|Valor devuelto|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
