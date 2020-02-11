---
title: Llamar a SQLSetPos para insertar datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e07bf71f0d622ad9095974cd7020001625edf1f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037708"
---
# <a name="calling-sqlsetpos-to-insert-data"></a>Llamar a SQLSetPos para insertar datos
Cuando una aplicación ODBC *2. x* que trabaja con un controlador ODBC *3. x* llama a **SQLSetPos** con un argumento de *operación* de SQL_ADD, el administrador de controladores no asigna esta llamada a **SQLBulkOperations**. Si un controlador ODBC *3. x* debe trabajar con una aplicación que llame a **SQLSetPos** con SQL_ADD, el controlador debe admitir esa operación.  
  
 Una diferencia importante en el comportamiento cuando se llama a **SQLSetPos** con SQL_ADD se produce cuando se llama en el estado S6. En ODBC *2. x*, el controlador devolvió S1010 cuando se llamó a **SQLSetPos** con SQL_ADD en el estado S6 (después de que el cursor se haya colocado con **SQLFetch**). En ODBC *3. x*, **SQLBulkOperations** con una *operación* de SQL_ADD se puede llamar en el estado S6. Una segunda diferencia importante en el comportamiento es que **SQLBulkOperations** con una *operación* de SQL_ADD se puede llamar en el estado S5, mientras que **SQLSetPos** con una **operación** de SQL_ADD no puede. En el caso de las transiciones de instrucciones que se pueden producir para la misma llamada en ODBC *3. x*, vea el [Apéndice B: tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
