---
title: SQUARE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f48770def142c5f01d580de5c9cd09573782f54
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="square-ssis-expression"></a>SQUARE (expresión de SSIS)
  Devuelve el cuadrado de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica de cualquier tipo de datos numérico. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Notas  
 SQUARE devuelve un resultado NULL si el valor del argumento es NULL.  
  
 Antes de realizar la operación de raíz cuadrada, se convierte el argumento al tipo de datos DT_R8.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve el cuadrado de 12. El resultado devuelto es 144.  
  
```  
SQUARE(12)  
```  
  
 Este ejemplo devuelve el cuadrado del resultado de restar los valores de dos columnas. Si **Value1** contiene 12 y **Value2** contiene 4, la función SQUARE devuelve 64.  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 Este ejemplo devuelve la longitud del tercer lado de un triángulo rectángulo aplicando la función SQUARE a dos variables y calculando a continuación la raíz cuadrada de la suma. Si **Side1** contiene 3 y **Side2** contiene 4, la función SQRT devuelve 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  En las expresiones, los nombres de variables siempre incluyen el prefijo @.  
  
## <a name="see-also"></a>Ver también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
