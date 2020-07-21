---
title: RIGHT (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1dcd15de93893b34a6842110767b2242fbc3a146
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297411"
---
# <a name="right-ssis-expression"></a>RIGHT (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Devuelve el número de caracteres especificado de la parte más a la derecha de la expresión de caracteres dada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RIGHT(character_expression,integer_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que se van a extraer caracteres.  
  
 *integer_expression*  
 Expresión entera que indica el número de caracteres que se van a devolver.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Observaciones  
 Si *integer_expression* es mayor que la longitud de *character_expression*, la función devuelve *character_expression*.  
  
 Si *integer_expression* es cero, la función devuelve una cadena de longitud cero.  
  
 Si *integer_expression* es un número negativo, la función devuelve un error.  
  
 El argumento *integer_expression* puede admitir variables y columnas.  
  
 RIGHT solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que RIGHT realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 RIGHT devuelve un resultado NULL si alguno de los argumentos es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En el siguiente ejemplo se utiliza un literal de cadena. El resultado devuelto es `"Bike"`.  
  
```  
RIGHT("Mountain Bike", 4)  
```  
  
 En el ejemplo siguiente se devuelve el número de caracteres situados más a la derecha que se especifica en la variable `Times` de la columna `Name` . Si `Name` es `Touring Front Wheel` y `Times` es 5, el resultado devuelto es `"Wheel"`.  
  
```  
RIGHT(Name, @Times)  
```  
  
 En el ejemplo siguiente también se devuelve el número de caracteres situados más a la derecha que se especifica en la variable `Times` de la columna `Name` . `Times` tiene un tipo de datos no entero y en la expresión se incluye una conversión explícita al tipo de datos DT_I2. Si `Name` es `Touring Front Wheel` y `Times` es `4.32`, el resultado devuelto es `"heel"` porque la función RIGHT convierte el valor de 4.32 a 4 y, a continuación, devuelve los cuatro caracteres situados más a la derecha.  
  
```  
RIGHT(Name, (DT_I2)@Times))  
```  
  
## <a name="see-also"></a>Consulte también  
 [LEFT &#40;expresión de SSIS&#41;](../../integration-services/expressions/left-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
