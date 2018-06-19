---
title: '- (Negar) (expresión de SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8c95e0c6dc3d53aa17bba45f7485abc96e69614
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35330649"
---
# <a name="--negate-ssis-expression"></a>- (Negativo) (expresión de SSIS)
  Niega una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión válida de cualquier tipo de datos numérico. Solo se admiten tipos de datos numéricos con signo. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos de *numeric_expression*.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo niega el valor de la variable **Counter** y le suma el literal numérico 50.  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>Ver también  
 [Precedencia y capacidad de asociación de operadores](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
