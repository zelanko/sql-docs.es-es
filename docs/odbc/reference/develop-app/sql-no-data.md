---
title: SQL_NO_DATA de la casa de la casa de Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299795"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Cuando un ODBC 3. *x* aplicación llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** en un ODBC 2. *x* controlador para ejecutar una instrucción de actualización o eliminación buscada que no afecta a ninguna fila en el origen de datos, el controlador debe devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando un ODBC 2. *x* u ODBC 3. *x* aplicación que trabaja con un ODBC 3. *x* controlador llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** con el mismo resultado, el ODBC 3. *x* controlador debe devolver SQL_NO_DATA.
