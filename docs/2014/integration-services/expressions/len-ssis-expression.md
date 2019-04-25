---
title: LEN (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a8bcaeb04bdc2ff8b37860ffc434d2e188436411
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769081"
---
# <a name="len-ssis-expression"></a>LEN (expresión de SSIS)
  Devuelve el número de caracteres de una expresión de caracteres. Si la cadena incluye espacios en blanco iniciales y finales, la función puede incluirlos en el recuento. LEN devuelve valores idénticos para la misma cadena de caracteres de byte único y de doble byte.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión que se va a evaluar.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_I4  
  
## <a name="remarks"></a>Comentarios  
 El argumento *character_expression* puede tener el tipo de datos DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE. Para obtener más información, vea [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
 Si *character_expression* es un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que LEN realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para más información, vea [Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md).  
  
 Si el argumento pasado a la función LEN tiene un tipo de datos de bloque de objetos binarios grandes (BLOB), como DT_TEXT, DT_NTEXT o DT_IMAGE, la función devuelve un número de bytes.  
  
 LEN devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve la longitud de un literal de cadena. El resultado devuelto es 12.  
  
```  
LEN("Ball Bearing")  
```  
  
 Este ejemplo devuelve la diferencia de longitud de los valores de las columnas **FirstName** y **LastName** .  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 Devuelve la longitud de un nombre de equipo utilizando la variable del sistema **MachineName**.  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
