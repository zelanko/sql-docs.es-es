---
title: SQLEndTran (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f713f9a0c96aaf3798cf160e648404470e3a4363
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064498"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLEndTran** función en la biblioteca de cursores. Para obtener información general sobre **SQLEndTran**, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 La biblioteca de cursores no admite transacciones y pasa las llamadas a **SQLEndTran** directamente al controlador. Sin embargo, la biblioteca de cursores es compatible con los comportamientos de confirmación y reversión del cursor devuelto por el origen de datos con los tipos de información SQL_CURSOR_ROLLBACK_BEHAVIOR y SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Orígenes de datos que conserva los cursores en las transacciones, los cambios que se revierten los cambios en el origen de datos no se revierten en memoria caché de la biblioteca de cursores. Para hacer que la memoria caché coincida con los datos del origen de datos, la aplicación debe cerrar y volver a abrir el cursor.  
  
-   Orígenes de datos que cierra los cursores en los límites de transacción, la biblioteca de cursores cierra los cursores y elimina las memorias caché de todas las instrucciones de la conexión.  
  
-   Orígenes de datos que eliminación las instrucciones preparadas en límites de la transacción, la aplicación debe reprepare todas las instrucciones preparadas en la conexión antes de ellos deteniéndose.
