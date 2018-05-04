---
title: SQLSetPos (biblioteca de cursores) | Documentos de Microsoft
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
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed803dd1663dc663e6badf324edf77d710a8912f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLSetPos** función en la biblioteca de cursores. Para obtener información general sobre **SQLSetPos**, consulte [SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 La biblioteca de cursores es compatible con la operación de SQL_POSITION solo para la *operación* argumento en **SQLSetPos**. Admite el valor SQL_LOCK_NO_CHANGE solo para la *LockType* argumento.  
  
 Si el controlador no admite las operaciones masivas, la biblioteca de cursores devuelve SQLSTATE HYC00 (no compatible con el controlador) cuando **SQLSetPos** se llama con *RowNumber* igual a 0. No se recomienda este comportamiento del controlador.  
  
 La biblioteca de cursores no admite las operaciones de SQL_UPDATE y SQL_DELETE en una llamada a **SQLSetPos**. Implementa la biblioteca de cursores una posición instrucción update o delete SQL mediante la creación de una búsqueda instrucción update o delete con una cláusula WHERE que enumera los valores almacenados en su caché para cada columna enlazada. Para obtener más información, consulte [procesar actualización coloca y eliminar instrucciones](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Si el controlador no es compatible con los cursores estáticos, debe llamar una aplicación trabajar con la biblioteca de cursores **SQLSetPos** sólo en un conjunto de filas recuperado por **SQLExtendedFetch** o **SQLFetchScroll** , no en **SQLFetch**. La biblioteca de cursores implementa **SQLExtendedFetch** y **SQLFetchScroll** mediante la realización de llamadas repetidas de **SQLFetch** (con un tamaño de conjunto de filas de 1) en el controlador. La biblioteca de cursores pasa las llamadas a **SQLFetch**, en la otra parte, a través del controlador. Si **SQLSetPos** se llama en un conjunto de filas de varias filas capturado por **SQLFetch** cuando el controlador no es compatible con los cursores estáticos, la llamada producirá un error porque **SQLSetPos** no funciona con cursores de solo avance. Esto sucederá incluso si una aplicación ha llamado correctamente **SQLSetStmtAttr** establecer SQL_ATTR_CURSOR_TYPE en SQL_CURSOR_STATIC, que la biblioteca de cursores admite incluso si el controlador no es compatible con los cursores estáticos.
