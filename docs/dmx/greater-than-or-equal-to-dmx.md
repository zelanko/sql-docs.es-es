---
title: '&gt;= (Mayor o igual que) (DMX) | Documentos de Microsoft'
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
dev_langs:
- DMX
helpviewer_keywords:
- '>= (greater than or equal to operator)'
- greater than or equal to (>=)
ms.assetid: a96b7e9c-72dc-4df1-aa41-85aad933df96
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 736cf2361101a9722aa3723c64a04f98fde04b0c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="gt-greater-than-or-equal-to-dmx"></a>&gt;= (Mayor o igual que) (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una operación de comparación que determina si el valor de una expresión DMX (Extensiones de minería de datos) es mayor o igual que el valor de otra expresión DMX.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DMX_Expression >= DMX_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DMX_Expression*  
 Expresión DMX válida.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que contiene TRUE si ambos parámetros son no NULL y el valor del primer parámetro es mayor o igual que el valor del segundo parámetro. El valor booleano contiene FALSE si ambos parámetros son no NULL y el valor del primer parámetro es menor que el valor del segundo parámetro. El valor booleano contiene un valor NULL si uno de los parámetros o ambos parámetros se evalúan como un valor NULL.  
  
## <a name="see-also"></a>Vea también  
 [Operadores de comparación &#40; DMX &#41;](../dmx/operators-comparison.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)  
  
  

