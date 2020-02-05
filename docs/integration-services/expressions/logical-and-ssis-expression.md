---
title: '&amp;&amp; (AND lógico) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cda41d0db42f72b56c84b184138ade1e345fdaa9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71289055"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (AND lógico) (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Realiza una operación lógica AND. La expresión devuelve TRUE si todas las condiciones son TRUE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
boolean_expression1 && boolean_expression2  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression1, boolean_expression2*  
 Cualquier expresión válida cuya evaluación devuelva TRUE, FALSE o NULL.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Observaciones  
 En la siguiente tabla se muestra el resultado del operador &&.  
  
|Resultado|Expression|Expression|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|FALSE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|NULL|NULL|TRUE|  
|FALSE|NULL|FALSE|  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En este ejemplo se usan las columnas **StandardCost** y **ListPrice** . Este ejemplo devuelve TRUE si el valor de la columna **StandardCost** es menor que 300 y el valor de la columna **ListPrice** es mayor que 500.  
  
```  
StandardCost < 300 && ListPrice > 500  
```  
  
 En este ejemplo se utilizan las variables **SPrice** y **LPrice** en lugar de literales.  
  
```  
StandardCost < @SPrice && ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Consulte también  
 [& &#40;AND bit a bit&#41; &#40;expresión de SSIS&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)   
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
