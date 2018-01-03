---
title: SQL_NO_DATA | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da9e5ffc19d884d2cb182190e11ba4dcf0a915bd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Cuando un ODBC 3. *x* aplicación llama **SQLExecDirect**, **SQLExecute**, o **SQLParamData** en una API ODBC 2. *x* controlador para ejecutar una actualización por búsqueda o delete, instrucción que no afecta a las filas del origen de datos, el controlador debería devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando un ODBC 2. *x* u ODBC 3. *x* aplicación trabajar con una aplicación ODBC 3. *x* controlador llama **SQLExecDirect**, **SQLExecute**, o **SQLParamData** con el mismo resultado, ODBC 3. *x* controlador debería devolver SQL_NO_DATA.
