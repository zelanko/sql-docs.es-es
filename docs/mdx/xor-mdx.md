---
title: XOR (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1657d9e58a0ae729a67e179602cd9a886ae923b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125789"
---
# <a name="xor-mdx"></a>XOR (MDX)


  Realiza una exclusión lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Una expresión MDX (Expresiones multidimensionales) válida que devuelve un valor numérico.  
  
 *Expression2*  
 Expresión MDX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **true** si uno y solo un argumento se evalúa como **true**; en caso contrario, **false**.  
  
## <a name="remarks"></a>Observaciones  
 El operador **XOR** trata ambos parámetros como valores booleanos (cero, 0, como **false**; de lo contrario, **true**) antes de que el operador realice la exclusión lógica. En la tabla siguiente se muestra cómo el operador **XOR** realiza la exclusión lógica.  
  
|*Expression1*|*Expression2*|Valor devuelto|  
|-------------------|-------------------|------------------|  
|**reales**|**reales**|**es**|  
|**reales**|**es**|**reales**|  
|**es**|**reales**|**reales**|  
|**es**|**es**|**es**|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
