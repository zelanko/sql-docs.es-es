---
title: SQLFreeStmt (biblioteca de cursores) | Documentos de Microsoft
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
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b648c069c3930e923db8a929f7203807c67b128e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLFreeStmt** función en la biblioteca de cursores. Para obtener información general sobre **SQLFreeStmt**, consulte [SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Si una aplicación llama **SQLFreeStmt** con la opción SQL_UNBIND después de llamar a **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**, la biblioteca de cursores devuelve un error. Antes de que pueden deshacer el enlace de columnas del conjunto de resultados, una aplicación debe llamar a **SQLCloseCursor** o **SQLFreeStmt** con la opción de SQL_CLOSE.

