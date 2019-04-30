---
title: Ejecución directa ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73c061718dc326e43f72be369a28ad12726a3cab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242359"
---
# <a name="direct-execution-odbc"></a>Ejecución directa ODBC
La ejecución directa es la manera más sencilla de ejecutar una instrucción. Cuando la instrucción se envía para su ejecución, el origen de datos lo compila en un plan de acceso y, a continuación, ejecuta ese plan de acceso.  
  
 Ejecución directa se utiliza normalmente en aplicaciones genéricas que compilación y ejecutan instrucciones en tiempo de ejecución. Por ejemplo, el código siguiente compila una instrucción SQL y lo ejecuta en una sola vez:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 Ejecución directa funciona mejor con las instrucciones que se va a ejecutar una sola vez. Su principal inconveniente es que la instrucción SQL se analiza cada vez que se ejecuta. Además, la aplicación no puede recuperar información sobre el conjunto de resultados creado por la instrucción (si existe) hasta que después se ejecuta la instrucción; Esto es posible si la instrucción se prepara y ejecuta en dos pasos independientes.  
  
 Para ejecutar una instrucción directamente, la aplicación realiza las acciones siguientes:  
  
1.  Establece los valores de los parámetros. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
2.  Las llamadas **SQLExecDirect** y le pasa una cadena que contiene la instrucción SQL.  
  
3.  Cuando **SQLExecDirect** se llama, el controlador:  
  
    -   Modifica la instrucción SQL para usar la gramática SQL del origen de datos sin analizar la instrucción; Esto incluye reemplazando las secuencias de escape se describe en [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). La aplicación puede recuperar el formulario de una instrucción SQL modificada mediante una llamada a **SQLNativeSql**. No se reemplazan las secuencias de escape si se establece el atributo de instrucción SQL_ATTR_NOSCAN.  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Envía la instrucción y los valores de parámetro convertido al origen de datos para su ejecución.  
  
    -   Devuelve los errores. Estos incluyen la secuenciación o diagnósticos de estado como SQLSTATE 24000 (estado de cursor no válido), los errores sintácticos, como SQLSTATE 42000 (sintaxis o infracción de acceso) y errores semánticos como SQLSTATE 42S02 (con Base en tabla o vista no encontrado).
