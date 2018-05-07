---
title: NO (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- NOT
dev_langs:
- DMX
helpviewer_keywords:
- NOT operator [DMX]
ms.assetid: 6d91b3d9-270c-4a68-b41f-169cff5faa0e
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 155dbc89f38ad39a87bbf2e69171e741735ec8a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="not-dmx"></a>NOT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Operador lógico que realiza una negación lógica de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Expresión DMX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve FALSE si el argumento se evalúa como TRUE; de lo contrario, devuelve TRUE.  
  
## <a name="remarks"></a>Comentarios  
 El argumento se trata como valor booleano (0 como FALSE; de lo contrario, TRUE) antes de que el operador realice la negación lógica. Si *Expression1* es TRUE, el operador devuelve FALSE. Si *Expression1* es FALSE, el operador devuelve TRUE. En la siguiente tabla se muestra cómo se realiza la conjunción lógica.  
  
|Si Expression1 es|El valor devuelto es|  
|-----------------------|---------------------|  
|TRUE|FALSE|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)  
  
  
