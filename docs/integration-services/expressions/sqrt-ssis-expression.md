---
title: "SQRT (expresión de SSIS) | Microsoft Docs"
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
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6176d42ed4c3537dcf49cdb6416c00cce37eed8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqrt-ssis-expression"></a>SQRT (expresión de SSIS)
  Devuelve la raíz cuadrada de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica de cualquier tipo de datos numérico. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Comentarios  
 SQRT devuelve un resultado NULL si el valor del argumento es NULL.  
  
 SQRT produce un error si el argumento es un valor negativo.  
  
 Antes de realizar la operación de raíz cuadrada, se convierte el argumento al tipo de datos DT_R8.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve la raíz cuadrada de un literal numérico. El resultado devuelto es 12.  
  
```  
SQRT(144)  
```  
  
 Este ejemplo devuelve la raíz cuadrada de una expresión, el resultado de restar valores de las columnas **Value1** y **Value2** .  
  
```  
SQRT(Value1 - Value2)  
```  
  
 Este ejemplo devuelve la longitud del tercer lado de un triángulo rectángulo aplicando la función SQUARE a dos variables y calculando a continuación la raíz cuadrada de la suma. Si **Side1** contiene 3 y **Side2** contiene 4, la función SQRT devuelve 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  En las expresiones, los nombres de variables siempre incluyen el prefijo @.  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
