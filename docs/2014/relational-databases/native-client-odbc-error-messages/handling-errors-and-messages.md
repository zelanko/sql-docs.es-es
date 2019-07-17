---
title: Controlar errores y mensajes | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4a4d87ccae235aee1a11e58aff60fe8e34d6205
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207091"
---
# <a name="handling-errors-and-messages"></a>Controlar errores y mensajes
  Cuando una aplicación llama a una función ODBC, el controlador ejecuta la función y devuelve información de diagnóstico de dos maneras: Un código de retorno indica el éxito o fracaso de una función ODBC general y los registros de diagnóstico proporcionan información detallada sobre la función. Los registros de diagnóstico incluyen un registro de encabezado y registros de estado. Por lo menos se devuelve un registro de diagnóstico, el registro de encabezado, aunque la función se ejecute correctamente.  
  
 La información de diagnóstico se usa en la fase de desarrollo para detectar errores de programación, como identificadores no válidos y errores de sintaxis en instrucciones SQL codificadas de forma rígida. También se utiliza en tiempo de ejecución para detectar errores y advertencias durante la ejecución, como truncamiento de datos, infracciones de reglas y errores de sintaxis en instrucciones SQL escritas por el usuario. La lógica del programa se suele basar en códigos de retorno.  
  
 Por ejemplo, después de una aplicación llama a **SQLFetch** para recuperar las filas de un conjunto de resultados, el código de retorno indica si se ha llegado al final del conjunto de resultados (SQL_NO_DATA), si los mensajes informativos se devolvieron (SQL_SUCCESS_ WITH_INFO), o si se ha producido un error (SQL_ERROR).  
  
 Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve algo distinto de SQL_SUCCESS, la aplicación puede llamar a **SQLGetDiagRec** para recuperar cualquier información o mensajes de error. Use **SQLGetDiagRec** para subir y Bajar el mensaje se establece si hay más de un mensaje.  
  
 El código de retorno SQL_INVALID_HANDLE siempre indica un error de programación y nunca debe encontrarse durante la ejecución. Todos los demás códigos de retorno proporcionan información en tiempo de ejecución, aunque SQL_ERROR puede indicar un error de programación.  
  
 La versión original [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API nativa, DB-Library para C, permite que una aplicación instalar el control de errores de devolución de llamada y el mensaje de control de las funciones que devuelven errores o mensajes. Algunas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], como PRINT, RAISERROR, DBCC y SET, devuelven sus resultados a la función de controlador de mensajes DB-Library en lugar de a un conjunto de resultados. Sin embargo, la API de ODBC no tiene ninguna capacidad de devolución de llamada semejante. Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client detecta mensajes procedentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Establece el código de retorno de ODBC en SQL_SUCCESS_WITH_INFO o SQL_ERROR y devuelve el mensaje como uno o más registros de diagnóstico. Por lo tanto, una aplicación ODBC debe comprobar cuidadosamente estos códigos de retorno y llamada **SQLGetDiagRec** para recuperar datos del mensaje.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Seguimiento de acceso a datos). Para obtener información acerca de las mejoras de seguimiento de errores que agregó en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Procesar instrucciones que generan mensajes](processing-statements-that-generate-messages.md)  
  
-   [Registros y campos de diagnóstico](diagnostic-records-and-fields.md)  
  
-   [Números de errores nativos](native-error-numbers.md)  
  
-   [SQLSTATE &#40;códigos de Error ODBC&#41;](sqlstate-odbc-error-codes.md)  
  
-   [Mensajes de error](error-messages.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
