---
title: Cierre el Cursor | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ea7b272ecf185efafed9b1b7b2209bbf7066369
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="closing-the-cursor"></a>Cierre el Cursor
Cuando una aplicación ha terminado de usar un cursor, se llama a **SQLCloseCursor** para cerrar el cursor. Por ejemplo:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Mientras el cursor cierra la aplicación, la instrucción en el que se abre el cursor no podrá usarse para la mayoría otras operaciones, como ejecutar otra instrucción SQL. Para obtener una lista completa de funciones que se puede llamar mientras el cursor está abierto, consulte [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para cerrar un cursor, una aplicación debe llamar a **SQLCloseCursor**, no **SQLCancel**.  
  
 Los cursores permanecen abiertos hasta que se cierran explícitamente, excepto cuando una transacción se confirma o revierte, en cuyo caso algunos orígenes de datos cierra el cursor. En concreto, llegando al final del resultado configurado, cuando **SQLFetch** devuelve SQL_NO_DATA, no se cierra un cursor. Incluso los cursores en los conjuntos de resultados vacíos (conjuntos de resultados creados cuando una instrucción ejecutada correctamente pero que no devuelve ninguna fila) se deben cerrar explícitamente.
