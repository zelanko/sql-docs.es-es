---
title: Códigos de retorno ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5f780f9abc47a367a1825d51b12159292ace5da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020422"
---
# <a name="return-codes-odbc"></a>Códigos de retorno de ODBC
Cada función de ODBC devuelve un código, conocido como *código de retorno,* que indica el éxito o error general de la función. La lógica del programa se suele basar en códigos de retorno.  
  
 Por ejemplo, el código siguiente llama a **SQLFetch** para recuperar las filas de un conjunto de resultados. Comprueba el código de retorno de la función para determinar si se ha alcanzado el final del conjunto de resultados (SQL_NO_DATA), si se ha devuelto alguna información de advertencia (SQL_SUCCESS_WITH_INFO) o si se ha producido un error (SQL_ERROR).  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 El código de retorno SQL_INVALID_HANDLE siempre indica un error de programación y nunca debe encontrarse durante la ejecución. Todos los demás códigos de retorno proporcionan información en tiempo de ejecución, aunque SQL_ERROR puede indicar un error de programación.  
  
 En la tabla siguiente se definen los códigos de retorno.  
  
|Código de retorno|Descripción|  
|-----------------|-----------------|  
|SQL_SUCCESS|La función se completó correctamente. La aplicación llama a **SQLGetDiagField** para recuperar información adicional del registro de encabezado.|  
|SQL_SUCCESS_WITH_INFO|La función se completó correctamente, posiblemente con un error no irrecuperable (ADVERTENCIA). La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional.|  
|SQL_ERROR|Error de la función. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional. El contenido de los argumentos de salida de la función es indefinido.|  
|SQL_INVALID_HANDLE|Error de la función debido a un entorno, una conexión, una instrucción o un identificador de descriptor no válidos. Esto indica un error de programación. No hay información adicional disponible desde **SQLGetDiagRec** o **SQLGetDiagField**. Este código solo se devuelve cuando el identificador es un puntero nulo o es un tipo incorrecto, como cuando se pasa un identificador de instrucción para un argumento que requiere un identificador de conexión.|  
|SQL_NO_DATA|No había más datos disponibles. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional. Es posible que se devuelvan uno o más registros de estado definidos por el controlador en la clase 02xxx. **Nota:**  En ODBC 2. *x*, este código de retorno se llamaba SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Se necesitan más datos, como cuando se envían datos de parámetros en tiempo de ejecución o se requiere información de conexión adicional. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional, si la hay.|  
|SQL_STILL_EXECUTING|Una función que se inició de forma asincrónica todavía se está ejecutando. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional, si la hay.|
