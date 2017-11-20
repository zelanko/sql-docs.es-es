---
title: Llamar a SQLSetPos para insertar datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e9d768ea5c16b199dc316726cb425b75d409bf1f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlsetpos-to-insert-data"></a>Llamar a SQLSetPos para insertar datos
Cuando un ODBC 2. *x* aplicación trabajar con una aplicación ODBC 3*.x* controlador llama **SQLSetPos** con una *operación* argumento de SQL_ADD, el Administrador de controladores no se asigna esta llamada a **SQLBulkOperations**. Si una aplicación ODBC 3*.x* controlador debería funcionar con una aplicación que llama **SQLSetPos** con SQL_ADD, el controlador debe admitir esa operación.  
  
 Una diferencia importante en el comportamiento cuando **SQLSetPos** se llama con SQL_ADD se produce cuando se llama en estado S6. En ODBC 2. *x*, el controlador devuelve S1010 cuando **SQLSetPos** se llamó con SQL_ADD en estado S6 (después de que se ha colocado el cursor con **SQLFetch**). En ODBC 3*.x*, **SQLBulkOperations** con una *operación* de SQL_ADD puede llamarse en estado S6. Una segunda diferencia importante en el comportamiento es que **SQLBulkOperations** con una *operación* de SQL_ADD puede ser llamado en estado S5, mientras **SQLSetPos** con un  **Operación** de SQL_ADD no puede. Para las transiciones de instrucción que pueden producirse en la misma llamada en ODBC 3*.x*, consulte [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).

