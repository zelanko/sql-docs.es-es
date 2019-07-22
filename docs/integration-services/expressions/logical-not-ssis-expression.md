---
title: '! (Not lógico) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 705f104eb6f3ab78f32a68af9277b2b4d9cef14d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027422"
---
# <a name="-logical-not-ssis-expression"></a>! (Not lógico) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Niega un operando booleano.  
  
> [!NOTE]  
>  El operador ! no se puede utilizar con otros operadores. Por ejemplo, los operadores ! y > no se pueden combinar para crear el operador !> .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Cualquier expresión válida que devuelva un valor booleano. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
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
  
 Este ejemplo devuelve TRUE si el valor de la variable **MonthNumber** es igual que el entero que representa el mes actual. Para más información, vea [MONTH &#40;expresión de SSIS&#41;](../../integration-services/expressions/month-ssis-expression.md) y [GETDATE &#40;expresión de SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>Consulte también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
