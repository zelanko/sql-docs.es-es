---
title: '|| (OR lógico) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e63c829e1865213b29aca6e75d1de52021b4d5ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052325"
---
# <a name="-logical-or-ssis-expression"></a>|| (OR lógico) (expresión de SSIS)
  Realiza una operación lógica OR. La expresión devuelve TRUE si una o ambas condiciones son TRUE.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression1, boolean_expression2*  
 Cualquier expresión válida cuya evaluación devuelva TRUE, FALSE o NULL.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentarios  
 En la siguiente tabla se muestra el resultado del operador ||.  
  
|Resultado|Expresión|Expresión|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## <a name="ssis-expression-examples"></a>Ejemplos de expresiones de SSIS  
 En este ejemplo se usan las columnas **StandardCost** y **ListPrice** . Este ejemplo devuelve TRUE si el valor de la columna **StandardCost** es menor que 300 o el valor de la columna **ListPrice** es mayor que 500.  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 En este ejemplo se utilizan las variables **SPrice** y **LPrice** en lugar de literales numéricos.  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>Vea también  
 [&#124;&#40;Bit a bit OR inclusivo&#41; &#40;expresión de SSIS&#41;](bitwise-inclusive-or-ssis-expression.md)   
 [^ &#40;OR exclusivo bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-exclusive-or-ssis-expression.md)   
 [Precedencia y asociatividad](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
