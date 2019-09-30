---
title: LN (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4bbf59211c35a6048c715594d9c298ba041bcf15
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289130"
---
# <a name="ln-ssis-expression"></a>LN (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve el logaritmo natural de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica distinta de cero y no negativa válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Notas  
 La expresión numérica se convierte al tipo de datos DT_R8 antes de que se calcule el logaritmo. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Si la evaluación de *numeric_expression* devuelve cero o un valor negativo, el resultado devuelto será NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal numérico. La función devuelve el valor 3,737766961828337.  
  
```  
LN(42)  
```  
  
 En este ejemplo se utiliza la columna **Length**. Si el valor de la columna is 53,99, la función devuelve 3,9887988442302.  
  
```  
LN(Length)   
```  
  
 En este ejemplo se utiliza la variable **Length**. La variable debe tener un tipo de datos numérico o la expresión debe incluir una conversión explícita a un tipo de datos numérico. Si el valor de **Length** es 234,567, la función devuelve 5.45774126708797.  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>Consulte también  
 [LOG &#40;expresión de SSIS&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
