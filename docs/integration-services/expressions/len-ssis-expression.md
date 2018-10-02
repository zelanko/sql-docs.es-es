---
title: LEN (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 09ef57d07b85f432e7b0ef4e4e814d5aa89a7979
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611323"
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
  
## <a name="remarks"></a>Notas  
 El argumento *character_expression* puede tener el tipo de datos DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE. Para más información, consulte [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Si *character_expression* es un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que LEN realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para más información, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
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
  
## <a name="see-also"></a>Ver también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
