---
title: Determinar el número de filas afectadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6a1bebf7d5cfb85e49fb0e382dacc4f4464054e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039981"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar el número de filas afectadas
Después de una aplicación actualiza, elimina o inserta filas, puede llamar a **SQLRowCount** para determinar el número de filas afectado. **SQLRowCount** devuelve este valor si las filas se han actualizado, eliminadas o insertado mediante la ejecución de un **actualización**, **eliminar**, o **insertar** instrucción, mediante la ejecución de un posicionadas update o delete, instrucción o al llamar a **SQLSetPos**.  
  
 Si se ejecuta un lote de instrucciones SQL, el recuento de filas afectadas podría ser un recuento total de todas las instrucciones del lote o recuentos individuales para cada instrucción del lote. Para obtener más información, consulte [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 También se devuelve el número de filas afectadas en el campo de encabezado diagnóstico SQL_DIAG_ROW_COUNT en el área de diagnóstico asociado con el identificador de instrucción. Sin embargo, los datos de este campo se restablecen después de llamar todas las funciones en el mismo identificador de instrucción, mientras que el valor devuelto por **SQLRowCount** sigue siendo la misma hasta que una llamada a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, o **SQLSetPos**.
