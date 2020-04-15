---
title: SQLEndTran (Biblioteca de cursores) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2277a67cd5410ea3c2a5d5b03b16d4533ed6ee1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304776"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLEndTran** en la biblioteca de cursores. Para obtener información general sobre **SQLEndTran**, vea [SqlEndTran (función)](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 La biblioteca de cursores no admite transacciones y pasa llamadas a **SQLEndTran** directamente al controlador. Sin embargo, la biblioteca de cursores admite los comportamientos de confirmación y reversión del cursor devueltos por el origen de datos con los tipos de información SQL_CURSOR_ROLLBACK_BEHAVIOR y SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Para los orígenes de datos que conservan los cursores en las transacciones, los cambios que se revierten en el origen de datos no se revierten en la memoria caché de la biblioteca de cursores. Para que la memoria caché coincida con los datos del origen de datos, la aplicación debe cerrar y volver a abrir el cursor.  
  
-   Para los orígenes de datos que cierran cursores en los límites de transacción, la biblioteca de cursores cierra los cursores y elimina las memorias caché de todas las instrucciones de la conexión.  
  
-   Para los orígenes de datos que eliminan instrucciones preparadas en los límites de transacción, la aplicación debe repreparar todas las instrucciones preparadas en la conexión antes de volver a ejecutarlas.
