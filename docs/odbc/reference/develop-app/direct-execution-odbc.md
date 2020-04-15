---
title: Ejecución directa ODBC (Direct Execution ODBC) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305166"
---
# <a name="direct-execution-odbc"></a>Ejecución directa ODBC
La ejecución directa es la forma más sencilla de ejecutar una instrucción. Cuando la instrucción se envía para su ejecución, el origen de datos la compila en un plan de acceso y, a continuación, ejecuta ese plan de acceso.  
  
 La ejecución directa se utiliza normalmente en aplicaciones genéricas que compilan y ejecutan instrucciones en tiempo de ejecución. Por ejemplo, el código siguiente crea una instrucción SQL y la ejecuta una sola vez:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 La ejecución directa funciona mejor para las instrucciones que se ejecutarán una sola vez. Su principal inconveniente es que la instrucción SQL se analiza cada vez que se ejecuta. Además, la aplicación no puede recuperar información sobre el conjunto de resultados creado por la instrucción (si existe) hasta después de ejecutar la instrucción; esto es posible si la instrucción se prepara y ejecuta en dos pasos separados.  
  
 Para ejecutar una instrucción directamente, la aplicación realiza las siguientes acciones:  
  
1.  Establece los valores de cualquier parámetro. Para obtener más información, consulte Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
2.  Llama a **SQLExecDirect** y le pasa una cadena que contiene la instrucción SQL.  
  
3.  Cuando se llama a **SQLExecDirect,** el controlador:  
  
    -   Modifica la instrucción SQL para utilizar la gramática SQL del origen de datos sin analizar la instrucción; Esto incluye la sustitución de las secuencias de escape descritas en [Secuencias](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)de escape en ODBC . La aplicación puede recuperar la forma modificada de una instrucción SQL llamando a **SQLNativeSql**. Las secuencias de escape no se reemplazan si se establece el atributo de instrucción SQL_ATTR_NOSCAN.  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, consulte Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Envía la instrucción y los valores de parámetro convertidos al origen de datos para su ejecución.  
  
    -   Devuelve los errores. Estos incluyen la secuenciación o diagnósticos de estado como SQLSTATE 24000 (estado de cursor no válido), errores sintácticos como SQLSTATE 42000 (error de sintaxis o infracción de acceso) y errores semánticos como SQLSTATE 42S02 (tabla base o vista no encontrada).
