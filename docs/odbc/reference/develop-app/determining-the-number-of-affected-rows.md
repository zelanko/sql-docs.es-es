---
title: Determinación del número de filas afectadas ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 156a5fe41d2c9b57a33bbc2bdb4540d1f5b00340
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305896"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar el número de filas afectadas
Después de que una aplicación actualiza, elimina o inserta filas, puede llamar a **SQLRowCount** para determinar cuántas filas se vieron afectadas. **SQLRowCount** devuelve este valor independientemente de si las filas se actualizaron, eliminaron o insertaron ejecutando una instrucción **UPDATE**, **DELETE**o **INSERT,** ejecutando una instrucción update o delete posicionada o llamando a **SQLSetPos**.  
  
 Si se ejecuta un lote de instrucciones SQL, el recuento de filas afectadas puede ser un recuento total para todas las instrucciones del lote o recuentos individuales para cada instrucción del lote. Para obtener más información, vea [Lotes de instrucciones SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y varios [resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 El número de filas afectadas también se devuelve en el campo de encabezado de diagnóstico SQL_DIAG_ROW_COUNT en el área de diagnóstico asociada con el identificador de instrucción. Sin embargo, los datos de este campo se restablecen después de cada llamada de función en el mismo identificador de instrucción, mientras que el valor devuelto por **SQLRowCount** sigue siendo el mismo hasta una llamada a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**o **SQLSetPos**.
