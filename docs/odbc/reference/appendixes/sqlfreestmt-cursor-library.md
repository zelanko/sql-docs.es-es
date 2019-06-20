---
title: SQLFreeStmt (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07d56e9b77c7e7e34b0de98ef5704b26aa2b86dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199464"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLFreeStmt** función en la biblioteca de cursores. Para obtener información general sobre **SQLFreeStmt**, consulte [función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Si una aplicación llama a **SQLFreeStmt** con la opción SQL_UNBIND después de llamar al **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**, la biblioteca de cursores devuelve un error. Antes de que pueden separar las columnas del conjunto de resultados, una aplicación debe llamar a **SQLCloseCursor** o **SQLFreeStmt** con la opción de SQL_CLOSE.
