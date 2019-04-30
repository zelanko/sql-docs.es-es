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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 986cd3c48104bfe822934eb415b854b8e976f242
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149123"
---
# <a name="status-records"></a>Registros de estado
Los campos de los registros de estado contienen información sobre errores específicos o las advertencias devueltos por el Administrador de controladores, controlador u origen de datos, incluidos SQLSTATE, el número de error nativo, mensaje de diagnóstico, número de columna y el número de fila. Registros de estado se pueden crear solo si la función devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Para obtener una lista completa de los campos de los registros de estado, consulte el [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) descripción de la función.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Secuencia de registros de estado](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md)
