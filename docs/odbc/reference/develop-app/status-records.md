---
title: Registros de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4afef16137404fcdfd3e1d328642f1d314829538
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301376"
---
# <a name="status-records"></a>Registros de estado
Los campos de los registros de estado contienen información sobre errores o advertencias específicos devueltos por el administrador de controladores, el controlador o el origen de datos, incluido SQLSTATE, el número de error nativo, el mensaje de diagnóstico, el número de columna y el número de fila. Los registros de estado solo se pueden crear si la función devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Para obtener una lista completa de los campos de los registros de estado, consulte la descripción de la función [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md)
