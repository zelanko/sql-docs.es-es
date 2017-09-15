---
title: SQLNativeSql (biblioteca de cursores) | Documentos de Microsoft
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
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c6062933f8f6d144b31da430788e8edd75da2eea
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLNativeSql** función en la biblioteca de cursores. Para obtener información general sobre **SQLNativeSql**, consulte [SQLNativeSql, función](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Si el controlador es compatible con esta función, llama a la biblioteca de cursores **SQLNativeSql** en el controlador y le pasa la instrucción SQL. Para actualización posicionada, coloca delete, y **seleccione para actualizar** instrucciones, la biblioteca de cursores modifica la instrucción antes de pasar al controlador.  
  
> [!NOTE]  
>  La biblioteca de cursores incorrectamente devuelve SQLSTATE 34000 (nombre de cursor no válido) si el nombre del cursor no es válido en una actualización por posición o una instrucción delete que se pasa en el *InStatementText* argumento de **SQLNativeSql **. **SQLNativeSql** no está diseñada para devolver errores de sintaxis, que se devuelven solo cuando la preparación o ejecución.
