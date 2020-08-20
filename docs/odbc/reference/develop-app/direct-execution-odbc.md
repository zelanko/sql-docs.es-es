---
description: Ejecución directa ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9be03c4f20a82e134481f8fd9bb849ffd830567a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476707"
---
# <a name="direct-execution-odbc"></a>Ejecución directa ODBC
La ejecución directa es la manera más sencilla de ejecutar una instrucción. Cuando la instrucción se envía para su ejecución, el origen de datos lo compila en un plan de acceso y, a continuación, ejecuta ese plan de acceso.  
  
 La ejecución directa se usa normalmente en aplicaciones genéricas que compilan y ejecutan instrucciones en tiempo de ejecución. Por ejemplo, el código siguiente crea una instrucción SQL y la ejecuta una sola vez:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 La ejecución directa funciona mejor para las instrucciones que se ejecutarán una sola vez. Su principal inconveniente es que la instrucción SQL se analiza cada vez que se ejecuta. Además, la aplicación no puede recuperar información sobre el conjunto de resultados creado por la instrucción (si existe) hasta que se ejecute la instrucción; Esto es posible si la instrucción se prepara y se ejecuta en dos pasos independientes.  
  
 Para ejecutar directamente una instrucción, la aplicación realiza las siguientes acciones:  
  
1.  Establece los valores de los parámetros. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
2.  Llama a **SQLExecDirect** y le pasa una cadena que contiene la instrucción SQL.  
  
3.  Cuando se llama a **SQLExecDirect** , el controlador:  
  
    -   Modifica la instrucción SQL para utilizar la gramática de SQL del origen de datos sin analizar la instrucción; Esto incluye reemplazar las secuencias de escape descritas en [secuencias de escape en ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). La aplicación puede recuperar el formulario modificado de una instrucción SQL mediante una llamada a **SQLNativeSql**. Las secuencias de escape no se reemplazan si se establece el atributo de instrucción SQL_ATTR_NOSCAN.  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Envía la instrucción y convierte los valores de parámetro en el origen de datos para su ejecución.  
  
    -   Devuelve cualquier error. Entre ellas se incluyen la secuenciación o el diagnóstico de estado, como SQLSTATE 24000 (estado de cursor no válido), errores sintácticos como SQLSTATE 42000 (error de sintaxis o infracción de acceso) y errores semánticos como SQLSTATE 42S02 (no se encontró la tabla base o la vista).
