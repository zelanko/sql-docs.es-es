---
title: SQLSetPos (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Cursor Library
ms.assetid: 574399c3-2bb2-4d19-829c-7c77bd82858d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c46ef88075a5adbd96138d7d1f03c26712f7ea1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300515"
---
# <a name="sqlsetpos-cursor-library"></a>SQLSetPos (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLSetPos** en la biblioteca de cursores. Para obtener información general acerca de **SQLSetPos**, vea [Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
 La biblioteca de cursores solo admite la operación SQL_POSITION para el argumento *Operation* en **SQLSetPos**. Admite el valor de SQL_LOCK_NO_CHANGE solo para el *LockType* argumento.  
  
 Si el controlador no admite operaciones masivas, la biblioteca de cursores devuelve SQLSTATE HYC00 (Driver not capable) cuando **SQLSetPos** se llama con *RowNumber* igual a 0. No se recomienda este comportamiento del controlador.  
  
 La biblioteca de cursores no admite las operaciones SQL_UPDATE y SQL_DELETE en una llamada a **SQLSetPos**. La biblioteca de cursores implementa una instrucción SQL de actualización o eliminación posicionada mediante la creación de una instrucción update o delete buscada con una cláusula WHERE que enumera los valores almacenados en su caché para cada columna enlazada. Para obtener más información, consulte Procesamiento de instrucciones de [actualización y eliminación posicionadas](../../../odbc/reference/appendixes/processing-positioned-update-and-delete-statements.md).  
  
 Si el controlador no admite cursores estáticos, una aplicación que trabaje con la biblioteca de cursores debe llamar a **SQLSetPos** solo en un conjunto de filas capturado por **SQLExtendedFetch** o **SQLFetchScroll**, no por **SQLFetch**. La biblioteca de cursores implementa **SQLExtendedFetch** y **SQLFetchScroll** realizando llamadas repetidas de **SQLFetch** (con un tamaño de conjunto de filas de 1) en el controlador. La biblioteca de cursores pasa las llamadas a **SQLFetch**, por otro lado, al controlador. Si **SQLSetPos** se llama en un conjunto de filas de varias filas capturado por **SQLFetch** cuando el controlador no admite cursores estáticos, se producirá un error en la llamada porque **SQLSetPos** no funciona con cursores de solo avance. Esto ocurrirá incluso si una aplicación ha llamado correctamente **SQLSetStmtAttr** para establecer SQL_ATTR_CURSOR_TYPE en SQL_CURSOR_STATIC, que admite la biblioteca de cursores incluso si el controlador no admite cursores estáticos.
