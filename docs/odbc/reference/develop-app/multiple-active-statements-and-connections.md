---
title: Varias instrucciones activas y las conexiones | Documentos de Microsoft
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
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97976df0d7f0a237abd2e67ed71202ba4d518f3b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="multiple-active-statements-and-connections"></a>Varias instrucciones activas y las conexiones
Algunos controladores y DBMS limitan el número de instrucciones y las conexiones que pueden estar activas al mismo tiempo. Estos números pueden ser tan pequeños como uno. Para obtener más información, vea las opciones SQL_MAX_CONCURRENT_ACTIVITIES y SQL_MAX_DRIVER_CONNECTIONS en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción, de la función y [controla la instrucción](../../../odbc/reference/develop-app/statement-handles.md) y [ Identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md).
