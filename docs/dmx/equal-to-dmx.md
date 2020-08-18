---
description: = (Igual a) (DMX)
title: = (Igual a) (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba57583c8af1b739335abc27c33eaaf2ea54dc1f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413362"
---
# <a name="-equal-to-dmx"></a>= (Igual a) (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Realiza una operación de comparación que determina si el valor de una expresión DMX (Extensiones de minería de datos) es igual que el valor de otra expresión DMX.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DMX_Expression = DMX_Expression   
```  
  
#### <a name="parameters"></a>Parámetros  
 *DMX_Expression*  
 Expresión DMX válida.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que contiene TRUE si ambos parámetros son no NULL y el valor del primer parámetro es igual que el valor del segundo parámetro. El valor booleano contiene FALSE si ambos parámetros son no NULL y el valor del primer parámetro es distinto del valor del segundo parámetro. El valor booleano contiene un valor NULL si uno de los parámetros o ambos parámetros se evalúan como un valor NULL.  
  
## <a name="see-also"></a>Consulte también  
 [Operadores de comparación &#40;DMX&#41;](../dmx/operators-comparison.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
