---
title: '- (Restar) (DMX) | Documentos de Microsoft'
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: 9602e908-e80c-442a-a412-073e10d0abd4
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6385e939f6dcf1881b86d9aa20d7f8e6c04aceb4
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="--subtract-dmx"></a>- (Restar) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza una operación aritmética que resta un número de otro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric_Expression - Numeric_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Numeric_expression*  
 Expresión DMX (Extensiones de minería de datos) válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor cuyo tipo de datos es el del parámetro con la mayor precedencia.  
  
## <a name="remarks"></a>Comentarios  
 Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra. Si una expresión se evalúa como un valor NULL, el operador devuelve el resultado de la otra expresión.  
  
## <a name="see-also"></a>Vea también  
 [Aritmética operadores &#40; DMX &#41;](../dmx/operators-arithmetic.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

