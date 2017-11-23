---
title: SQLEndTran (biblioteca de cursores) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7ca0f1299933293990fc2c977a4a6602f9d4400
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLEndTran** función en la biblioteca de cursores. Para obtener información general sobre **SQLEndTran**, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 La biblioteca de cursores no admite transacciones y pasa las llamadas a **SQLEndTran** directamente en el controlador. Sin embargo, la biblioteca de cursores es compatible con los comportamientos de commit y rollback del cursor devuelto por el origen de datos con los tipos de información SQL_CURSOR_ROLLBACK_BEHAVIOR y SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Para los orígenes de datos que conservan los cursores a través de las transacciones, los cambios que se revierten los cambios en el origen de datos no se revierten en memoria caché de la biblioteca de cursores. Para hacer que la memoria caché coincida con los datos del origen de datos, la aplicación debe cerrar y volver a abrir el cursor.  
  
-   Para orígenes de datos que cierra los cursores en los límites de transacción, la biblioteca de cursores cierra los cursores y elimina las memorias caché para todas las instrucciones de la conexión.  
  
-   Para los orígenes de datos que se eliminan mediante instrucciones preparadas en límites de la transacción, la aplicación debe reprepare en la conexión antes de volver a ejecutar ellos todas las instrucciones preparadas.
