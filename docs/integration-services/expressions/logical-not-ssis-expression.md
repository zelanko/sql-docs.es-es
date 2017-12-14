---
title: "! (Not lógico) (expresión de SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8c6c84a9efe60ffc7d9ebda818ddeabf833d05a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
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
 Cualquier expresión válida que devuelva un valor booleano. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentarios  
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
  
 Este ejemplo devuelve TRUE si el valor de la variable **MonthNumber** es igual que el entero que representa el mes actual. Para más información, vea [MONTH &#40;expresión de SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md) y [GETDATE &#40;expresión de SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
