---
title: SQLSetScrollOptions (biblioteca de cursores) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c029dbb9906c4d7d738e0e705dd02e437b6c1bec
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLSetScrollOptions** función en la biblioteca de cursores. Para obtener información general sobre **SQLSetScrollOptions**, consulte [SQLSetScrollOptions función](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 La biblioteca de cursores es compatible con **SQLSetScrollOptions** solo por compatibilidad con versiones anteriores; aplicaciones deben utilizar los atributos de instrucción SQL_ATTR_ROW_ARRAY_SIZE, SQL_ATTR_CURSOR_TYPE y SQL_ATTR_CONCURRENCY en su lugar.
