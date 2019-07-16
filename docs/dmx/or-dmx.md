---
title: O (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 76b1f8ac9a5f7ad584f42110f2c3b22e5c1918ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008144"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que realiza una disyunción lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 OR Expression2  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Expresión DMX (Extensiones de minería de datos) válida que devuelve un valor numérico.  
  
 *Expression2*  
 Expresión DMX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor booleano que devuelve TRUE si uno de los dos argumentos o ambos argumentos se evalúan como TRUE; de lo contrario, devuelve FALSE.  
  
## <a name="remarks"></a>Comentarios  
 Ambos argumentos se tratan como valores booleanos (0 como FALSE; de lo contrario, TRUE) antes de que el operador realice la disyunción lógica. Si uno de los dos argumentos o ambos argumentos se evalúan como TRUE, el operador devuelve TRUE. Si *Expression1* se evalúa como TRUE y *Expression2* se evalúa como FALSE, el operador devuelve TRUE.  
  
 En la siguiente tabla se muestra cómo se realiza la disyunción lógica.  
  
|Si Expression1 es|Si Expression2 es|El valor devuelto es|  
|-----------------------|-----------------------|---------------------|  
|TRUE|TRUE|TRUE|  
|TRUE|FALSE|TRUE|  
|FALSE|TRUE|TRUE|  
|FALSE|FALSE|FALSE|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operators &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
