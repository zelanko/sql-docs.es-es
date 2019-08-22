---
title: Control de errores | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6277b3ecf0160078fa47bc79994d31f64519d9b7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028027"
---
# <a name="handling-errors"></a>Control de errores
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], todas las condiciones de error de la base de datos se devuelven a la aplicación Java como excepciones mediante la clase [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). Los siguientes métodos de la clase SQLServerException están heredados de java.sql.SQLException y java.lang.Throwable y se pueden emplear para devolver información específica sobre el error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ha producido:  
  
-   `getSQLState()` devuelve el código de estado X/Open o SQL99 de la excepción.
  
-   `getErrorCode()` devuelve el número específico del error de la base de datos.
  
-   `getMessage()` devuelve el texto completo de la excepción. El texto del mensaje de error describe el problema y, con frecuencia, incluye marcadores de posición de información tales como nombres de objetos, que se incluyen en el mensaje de error cuando se muestra.
  
-   `getNextException()` devuelve el siguiente objeto `SQLServerException` o nulo si no hay más objetos de excepción que devolver.

-   `getSQLServerError()`Devuelve el `SQLServerError` objeto que contiene información detallada sobre la excepción como recibida de SQL Server. Este método devuelve NULL si no se ha producido ningún error del servidor.

Los siguientes métodos de la `SQLServerError` clase se pueden utilizar para obtener detalles adicionales sobre el error generado desde el servidor.

-   `SQLServerError.getErrorMessage()`Devuelve el mensaje de error tal y como se recibe del servidor.

-   `SQLServerError.getErrorNumber()`Devuelve un número que identifica el tipo de error.

-   `SQLServerError.getErrorState()`Devuelve un código de error numérico desde SQL Server que representa un mensaje de error, ADVERTENCIA o "no se encontraron datos".

-   `SQLServerError.getErrorSeverity()`Devuelve el nivel de gravedad del error recibido.

-   `SQLServerError.getServerName()`Devuelve el nombre del equipo que ejecuta una instancia de SQL Server que generó el error.

-   `SQLServerError.getProcedureName()`Devuelve el nombre del procedimiento almacenado o llamada a procedimiento remoto (RPC) que generó el error.

-   `SQLServerError.getLineNumber()`Devuelve el número de línea del procedimiento almacenado o lote de comandos de Transact-SQL que generó el error.
  
 En el siguiente ejemplo, se pasa a la función una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] y se construye una instrucción SQL incorrecta que no incluye una cláusula FROM. A continuación, se ejecuta la instrucción de SQL y se procesa una excepción de SQL.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Diagnóstico de problemas del controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
