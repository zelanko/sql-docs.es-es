---
title: Cerrando el cursor ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299145"
---
# <a name="closing-the-cursor"></a>Cierre el Cursor
Cuando una aplicación ha terminado de usar un cursor, llama a **SQLCloseCursor** para cerrar el cursor. Por ejemplo:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Hasta que la aplicación cierra el cursor, la instrucción en la que se abre el cursor no se puede utilizar para la mayoría de las otras operaciones, como ejecutar otra instrucción SQL. Para obtener una lista completa de las funciones a las que se puede llamar mientras un cursor está abierto, consulte [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .  
  
> [!NOTE]  
>  Para cerrar un cursor, una aplicación debe llamar a **SQLCloseCursor**, no **SQLCancel**.  
  
 Los cursores permanecen abiertos hasta que se cierran explícitamente, excepto cuando se confirma o revierte una transacción, en cuyo caso algunos orígenes de datos cierran el cursor. En particular, llegar al final del conjunto de resultados, cuando **SQLFetch** devuelve SQL_NO_DATA, no cierra un cursor. Incluso los cursores en conjuntos de resultados vacíos (conjuntos de resultados creados cuando una instrucción se ejecutó correctamente pero que no devolvió ninguna fila) deben cerrarse explícitamente.
