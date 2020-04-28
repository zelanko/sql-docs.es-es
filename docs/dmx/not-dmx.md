---
title: NO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b4a28c6be2c956636f303ccc561936f799c63b64
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68008250"
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que realiza una negación lógica de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Argumento*  
 Expresión DMX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve FALSE si el argumento se evalúa como TRUE; de lo contrario, devuelve TRUE.  
  
## <a name="remarks"></a>Observaciones  
 El argumento se trata como valor booleano (0 como FALSE; de lo contrario, TRUE) antes de que el operador realice la negación lógica. Si *expression1* es true, el operador devuelve false. Si *expression1* es false, el operador devuelve true. En la siguiente tabla se muestra cómo se realiza la conjunción lógica.  
  
|Si Expression1 es|El valor devuelto es|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
