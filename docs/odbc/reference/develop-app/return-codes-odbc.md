---
title: "Códigos de retorno ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b997bfd1cc338f9c7a9dbb4b1b5b1ce851e71072
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="return-codes-odbc"></a>Códigos de retorno de ODBC
Cada función de ODBC devuelve un código, conocido como su *código devuelto,* que indica el éxito o fracaso de la función global. La lógica del programa se suele basar en códigos de retorno.  
  
 Por ejemplo, el código siguiente llama **SQLFetch** para recuperar las filas en un conjunto de resultados. Comprueba el código de retorno de la función para determinar si se alcanzó el final del conjunto de resultados (SQL_NO_DATA), si se devolvió ninguna información de advertencia (SQL_SUCCESS_WITH_INFO) o si produjo un error (SQL_ERROR).  
  
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
  
 En la tabla siguiente define los códigos de retorno.  
  
|Código de retorno|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|Función se completó correctamente. La aplicación llama **SQLGetDiagField** para recuperar información adicional desde el registro de encabezado.|  
|SQL_SUCCESS_WITH_INFO|Función que se completó correctamente, posiblemente con un error recuperable (advertencia). La aplicación llama **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional.|  
|SQL_ERROR|Error de la función. La aplicación llama **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional. El contenido de cualquier parámetro de salida a la función es indefinido.|  
|SQL_INVALID_HANDLE|Error en la función debido a un identificador de entorno, conexión, instrucción o descriptor no válido. Esto indica un error de programación. No hay información adicional está disponible en **SQLGetDiagRec** o **SQLGetDiagField**. Este código se devuelve solo cuando el identificador es un puntero nulo o no es del tipo correcto, por ejemplo, cuando se pasa un identificador de instrucción para un argumento que requiera un identificador de conexión.|  
|SQL_NO_DATA|No hay más datos estuvieran disponibles. La aplicación llama **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional. Se pueden devolver uno o más registros de estado definidos por el controlador de clase 02xxx. **Nota:** en ODBC 2. *x*, este valor devuelto de código se denominaba SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Se necesitan más datos, por ejemplo, cuando se envían los datos de parámetro en tiempo de ejecución o se necesita información de conexión adicionales. La aplicación llama **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional, si lo hay.|  
|SQL_STILL_EXECUTING|Todavía se está ejecutando una función que se inicia de forma asincrónica. La aplicación llama **SQLGetDiagRec** o **SQLGetDiagField** para recuperar información adicional, si lo hay.|

