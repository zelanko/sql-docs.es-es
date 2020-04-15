---
title: Llamar a SQLSetPos para insertar datos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], inserting data
- backward compatibility [ODBC], SqlSetPos
ms.assetid: 03e5c4d0-2bb3-4649-9781-89cab73f78eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb374b2506d55b400207c8f60bdf42bb6bb4065e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306606"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Llamar a SQLSetPos para insertar datos
Cuando una aplicación ODBC *2.x* que trabaja con un controlador ODBC *3.x* llama a **SQLSetPos** con un *operación* argumento de SQL_ADD, el Administrador de controladores no asigna esta llamada a **SQLBulkOperations**. Si un controlador ODBC *3.x* debe funcionar con una aplicación que llama a **SQLSetPos** con SQL_ADD, el controlador debe admitir esa operación.  
  
 Una diferencia importante en el comportamiento cuando **SQLSetPos** se llama con SQL_ADD se produce cuando se llama en el estado S6. En ODBC *2.x*, el controlador devolvió S1010 cuando **sqlSetPos** se llamó con SQL_ADD en el estado S6 (después de que el cursor se ha colocado con **SQLFetch**). En ODBC *3.x*, **SQLBulkOperations** con una *operación* de SQL_ADD se puede llamar en el estado S6. Una segunda diferencia importante en el comportamiento es que **SQLBulkOperations** con una *operación* de SQL_ADD se puede llamar en el estado S5, mientras que **SQLSetPos** con una **operación** de SQL_ADD no puede. Para las transiciones de instrucción que pueden producirse para la misma llamada en ODBC *3.x*, vea [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .
