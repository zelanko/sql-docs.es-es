---
title: SQRT (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQRT function
- square root of given expression
ms.assetid: 54a75389-c501-4e22-87b8-905f66d6a3a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 308a74501b0b4bf7b071feae2088c1ab1b7f030c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62768771"
---
# <a name="sqrt-ssis-expression"></a>SQRT (expresión de SSIS)
  Devuelve la raíz cuadrada de una expresión numérica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQRT(numeric_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica de cualquier tipo de datos numérico. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Observaciones  
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
>  En las expresiones, los nombres de variables siempre incluyen el prefijo \@.  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
