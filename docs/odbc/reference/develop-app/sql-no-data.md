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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a399a270eb1cd2f3daf9449c53b1f577a6b9545
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299795"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Cuando se trata de un ODBC 3. la aplicación *x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** en ODBC 2. controlador *x* para ejecutar una instrucción UPDATE o DELETE buscada que no afecte a ninguna fila del origen de datos, el controlador debe devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando se trata de un ODBC 2. *x* o ODBC 3. aplicación *x* que trabaja con ODBC 3. el controlador *x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** con el mismo resultado, ODBC 3. el controlador *x* debe devolver SQL_NO_DATA.
