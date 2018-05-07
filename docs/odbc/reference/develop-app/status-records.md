---
title: Registros de estado | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d36b40394f3f968f2ab841006a82b7ccb2218bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="status-records"></a>Registros de estado
Los campos de los registros de estado contienen información sobre errores específicos o las advertencias devueltos por el Administrador de controladores, controlador u origen de datos, incluidos el SQLSTATE, el número de error nativo, mensaje de diagnóstico, número de columna y número de fila. Registros de estado se pueden crear solo si la función devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Para obtener una lista completa de campos de los registros de estado, consulte la [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md)
