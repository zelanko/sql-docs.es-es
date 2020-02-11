---
title: Cerrar el cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036545"
---
# <a name="closing-the-cursor"></a>Cierre el Cursor
Cuando una aplicación ha terminado de usar un cursor, llama a **SQLCloseCursor** para cerrar el cursor. Por ejemplo:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Hasta que la aplicación cierre el cursor, la instrucción en la que se abre el cursor no se puede usar para la mayoría de las demás operaciones, como la ejecución de otra instrucción SQL. Para obtener una lista completa de las funciones a las que se puede llamar mientras se abre un cursor, vea [Apéndice B: tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Para cerrar un cursor, una aplicación debe llamar a **SQLCloseCursor**, no a **SQLCancel**.  
  
 Los cursores permanecen abiertos hasta que se cierran explícitamente, excepto cuando una transacción se confirma o se revierte, en cuyo caso algunos orígenes de datos cierran el cursor. En concreto, al llegar al final del conjunto de resultados, cuando **SQLFetch** devuelve SQL_NO_DATA, no cierra un cursor. Incluso los cursores en conjuntos de resultados vacíos (los conjuntos de resultados creados cuando una instrucción se ejecuta correctamente pero que no devuelven filas) deben cerrarse explícitamente.
