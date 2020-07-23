---
title: Y (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ea3cacd8fe2d80e6037cf83df9eea1fd112a4b05
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971838"
---
# <a name="and-dmx"></a>AND (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Realiza una conjunción lógica de dos expresiones numéricas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 AND Expression2  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Expresión DMX (Extensiones de minería de datos) válida que devuelve un valor numérico.  
  
 *Expression2*  
 Expresión DMX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve TRUE si los dos parámetros se evalúan como TRUE; de lo contrario, devuelve FALSE.  
  
## <a name="remarks"></a>Observaciones  
 Ambos parámetros se tratan como valores booleanos (0 como FALSE; de lo contrario, TRUE) antes de que el operador realice la conjunción lógica. En la siguiente tabla se muestran los valores devueltos en función de las diversas combinaciones de valores de parámetro.  
  
|Si Expression1 es|Si Expression2 es|El valor devuelto es|  
|-----------------------|-----------------------|---------------------|  
|VERDADERO|VERDADERO|VERDADERO|  
|TRUE|FALSE|FALSE|  
|FALSO|VERDADERO|FALSE|  
|FALSE|FALSE|FALSO|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
