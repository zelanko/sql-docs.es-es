---
title: O (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OR
dev_langs:
- DMX
helpviewer_keywords:
- OR operator
ms.assetid: 727a38a9-7f75-4963-8e8a-aa703c129d30
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 41cdd1638dc31eefa9cb034db33ef9d30162d617
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="or-dmx"></a>OR (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Lógico operadores &#40; DMX &#41;](../dmx/operators-logical.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

