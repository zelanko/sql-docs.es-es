---
title: O (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 21ac78f6ee0ed77bb9549f1749d73d29344a49d1
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86968459"
---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

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
  
## <a name="remarks"></a>Observaciones  
 Ambos argumentos se tratan como valores booleanos (0 como FALSE; de lo contrario, TRUE) antes de que el operador realice la disyunción lógica. Si uno de los dos argumentos o ambos argumentos se evalúan como TRUE, el operador devuelve TRUE. Si *expression1* se evalúa como true y *expression2* se evalúa como false, el operador devuelve true.  
  
 En la siguiente tabla se muestra cómo se realiza la disyunción lógica.  
  
|Si Expression1 es|Si Expression2 es|El valor devuelto es|  
|-----------------------|-----------------------|---------------------|  
|VERDADERO|VERDADERO|VERDADERO|  
|TRUE|FALSO|VERDADERO|  
|FALSO|VERDADERO|TRUE|  
|FALSE|FALSE|FALSO|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
