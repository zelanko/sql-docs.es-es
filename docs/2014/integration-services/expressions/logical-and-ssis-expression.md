---
title: '&amp;&amp; (AND lógico) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- '&& (logical AND)'
- AND, logical AND
- logical AND (&&)
ms.assetid: a8cb3517-d5d1-4861-9f04-905c719185ff
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9f6cdb28a48a69ee1702b19918b9326ac861eb29
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105161"
---
# <a name="ampamp-logical-and-ssis-expression"></a>&amp;&amp; (AND lógico) (expresión de SSIS)
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
  
## <a name="remarks"></a>Notas  
 En la siguiente tabla se muestra el resultado del operador &&.  
  
|Resultado|Expresión|Expresión|  
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
  
## <a name="see-also"></a>Vea también  
 [& &#40;AND bit a bit&#41; &#40;expresión de SSIS&#41;](bitwise-and-ssis-expression.md)   
 [Prioridad y asociatividad](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  