---
title: Devolver códigos de ODBC | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020422"
---
# <a name="return-codes-odbc"></a>Códigos de retorno de ODBC
Cada función de ODBC devuelve un código, conocido como su *código de retorno y* que indica el éxito o fracaso de la función global. La lógica del programa se suele basar en códigos de retorno.  
  
 Por ejemplo, el siguiente código llama a **SQLFetch** para recuperar las filas en un conjunto de resultados. Comprueba el código de retorno de la función para determinar si se alcanzó el final del conjunto de resultados (SQL_NO_DATA), si se devolvió ninguna información de advertencia (SQL_SUCCESS_WITH_INFO) o si se ha producido un error (SQL_ERROR).  
  
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
  
 La siguiente tabla define los códigos de retorno.  
  
|Código de retorno|Descripción|  
|-----------------|-----------------|  
|SQL_SUCCESS|Función se completó correctamente. La aplicación llama a **SQLGetDiagField** para recuperar información adicional desde el registro de encabezado.|  
|SQL_SUCCESS_WITH_INFO|Función que se ha completado correctamente, posiblemente con un error recuperable (advertencia). La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional.|  
|SQL_ERROR|Error de la función. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional. El contenido de cualquier parámetro de salida a la función es indefinido.|  
|SQL_INVALID_HANDLE|Función falló debido a un identificador de entorno, conexión, instrucción o descriptor no válido. Esto indica un error de programación. No hay información adicional está disponible en **SQLGetDiagRec** o **SQLGetDiagField**. Este código solo se devuelve cuando el identificador es un puntero nulo o no es del tipo correcto, por ejemplo, cuando se pasa un identificador de instrucción para un argumento que requiere un identificador de conexión.|  
|SQL_NO_DATA|No hay más datos no estaban disponibles. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional. Se pueden devolver uno o más registros de estado definidos por el controlador de clase 02xxx. **Nota:**  En ODBC 2. *x*, este devolverá el código se denominaba SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Se necesitan más datos, por ejemplo, cuando se envían los datos del parámetro en tiempo de ejecución o se necesita información de conexión adicionales. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional, si existe.|  
|SQL_STILL_EXECUTING|Todavía se está ejecutando una función que se inició de forma asincrónica. La aplicación llama a **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional, si existe.|
