---
title: SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 749351694a41764b9b5cc8bf3421340d62626aaf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62445967"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Cuando un ODBC 3. *x* aplicación llama a **SQLExecDirect**, **SQLExecute**, o **SQLParamData** en un ODBC 2. *x* controlador para ejecutar una actualización por búsqueda o eliminar la instrucción que no afecta a todas las filas en el origen de datos, el controlador debe devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando un ODBC 2. *x* u ODBC 3. *x* la aplicación funciona con una aplicación ODBC 3. *x* controlador llama a **SQLExecDirect**, **SQLExecute**, o **SQLParamData** con el mismo resultado, el ODBC 3. *x* controlador debería devolver SQL_NO_DATA.
