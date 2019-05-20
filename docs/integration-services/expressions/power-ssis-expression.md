---
title: POWER (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4515d920039c6dacd48e4b969928d525a1cec67
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725052"
---
# <a name="power-ssis-expression"></a>POWER (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve el resultado de elevar una expresión numérica a una determinada potencia. La evaluación del parámetro de potencia debe devolver un entero.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Expresión numérica válida.  
  
 *power*  
 Expresión numérica válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_R8  
  
## <a name="remarks"></a>Notas  
 Los argumentos *numeric_expression* y *power* se convierten al tipo de datos DT_R8 antes de que se calcule la potencia. Para obtener más información, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Si el valor de *numeric_expression* da como resultado cero y el valor de *power* es negativo, el evaluador de expresiones devolverá un error y establecerá el resultado devuelto en NULL.  
  
 Si *numeric_expression* o *power* producen resultados indeterminados, el resultado devuelto será NULL.  
  
 El argumento *power* puede ser una fracción. Por ejemplo, puede utilizar el valor 0,5 como potencia.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal numérico. La función eleva 4 a la potencia 3 y devuelve 64.  
  
```  
POWER(4,3)  
```  
  
 Este ejemplo utiliza la columna **Length** y la variable **DimensionCount** . Si el valor de **Length** es 8 y el de **DimensionCount** es 2, el resultado devuelto es 64.  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
