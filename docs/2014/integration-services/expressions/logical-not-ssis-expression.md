---
title: '! (Not lógico) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 119efb0b0957e55c1563d193593854cebfb87524
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213395"
---
# <a name="-logical-not-ssis-expression"></a>! (Not lógico) (expresión de SSIS)
  Niega un operando booleano.  
  
> [!NOTE]  
>  El operador ! no se puede utilizar con otros operadores. Por ejemplo, los operadores ! y > no se pueden combinar para crear el operador !> .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Cualquier expresión válida que devuelva un valor booleano. Para más información, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Notas  
 La siguiente tabla muestra el resultado de la operación de publicación.  
  
|Expresión booleana original|Después de aplicar ! como operador|  
|---------------------------------|------------------------------------|  
|TRUE|FALSE|  
|NULL|NULL|  
|FALSE|TRUE|  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En este ejemplo se devuelve FALSE si el valor de la columna **Color** es "red".  
  
```  
!(Color == "red")  
```  
  
 Este ejemplo devuelve TRUE si el valor de la variable **MonthNumber** es igual que el entero que representa el mes actual. Para más información, vea [MONTH &#40;expresión de SSIS&#41;](month-ssis-expression.md) y [GETDATE &#40;expresión de SSIS&#41;](getdate-ssis-expression.md).  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y asociatividad](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
