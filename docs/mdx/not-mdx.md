---
description: NOT (MDX)
title: NOT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c0cfa43896457397f2e2e08bac0b3de1d61e73f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471787"
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
 Valor booleano que devuelve **false** si el argumento se evalúa como **true**; en caso contrario, **true**.  
  
## <a name="remarks"></a>Observaciones  
 El operador **Not** trata la expresión como un valor booleano (cero, 0, como **false**; de lo contrario, **true**) antes de que el operador realice la negación lógica. En la tabla siguiente se muestra cómo el operador **Not** realiza la negación lógica.  
  
|*Expression1*|Valor devuelto|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
