---
title: Determinar el número de filas afectadas | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b826520d76b36eefab78de7e1d9db34ed202fb6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar el número de filas afectadas
Después de que una aplicación actualiza, elimina o inserta filas, puede llamar a **SQLRowCount** para determinar el número de filas afectado. **SQLRowCount** devuelve este valor o no las filas se han actualizado, eliminadas o insertadas mediante la ejecución de un **actualización**, **eliminar**, o **insertar** (instrucción), mediante la ejecución de una posición update o delete, instrucción o mediante una llamada a **SQLSetPos**.  
  
 Si se ejecuta un lote de instrucciones SQL, el recuento de filas afectadas podría ser un número total de todas las instrucciones del lote o recuentos individuales para cada instrucción del lote. Para obtener más información, consulte [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 También se devuelve el número de filas afectadas en el campo de encabezado diagnóstico SQL_DIAG_ROW_COUNT en el área de diagnóstico asociado con el identificador de instrucción. Sin embargo, los datos de este campo se restablecen después de llamar cada función en el mismo identificador de instrucción, mientras que el valor devuelto por **SQLRowCount** sigue siendo la misma hasta que una llamada a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, o **SQLSetPos**.
