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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039981"
---
# <a name="determining-the-number-of-affected-rows"></a>Determinar el número de filas afectadas
Después de que una aplicación actualiza, elimina o inserta filas, puede llamar a **SQLRowCount** para determinar el número de filas afectadas. **SQLRowCount** devuelve este valor si las filas se actualizaron, eliminaron o insertaron mediante la ejecución de una instrucción **Update**, **Delete**o **Insert** , ejecutando una instrucción UPDATE o DELETE posicionada o llamando a **SQLSetPos**.  
  
 Si se ejecuta un lote de instrucciones SQL, el recuento de filas afectadas podría ser un recuento total de todas las instrucciones del lote o recuentos individuales para cada instrucción del lote. Para obtener más información, vea [lotes de instrucciones SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md) y [varios resultados](../../../odbc/reference/develop-app/multiple-results.md).  
  
 El número de filas afectadas también se devuelve en el campo SQL_DIAG_ROW_COUNT encabezado de diagnóstico en el área de diagnóstico asociada al identificador de instrucción. Sin embargo, los datos de este campo se restablecen después de cada llamada de función en el mismo identificador de instrucción, mientras que el valor devuelto por **SQLRowCount** permanece igual hasta una llamada a **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**o **SQLSetPos**.
