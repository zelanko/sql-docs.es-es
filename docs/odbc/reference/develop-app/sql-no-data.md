---
description: SQL_NO_DATA
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
ms.openlocfilehash: eb81d6f1fce50a27aba203eec4b78648754010e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424577"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Cuando se trata de un ODBC 3. la aplicación *x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** en ODBC 2. controlador *x* para ejecutar una instrucción UPDATE o DELETE buscada que no afecte a ninguna fila del origen de datos, el controlador debe devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando se trata de un ODBC 2. *x* o ODBC 3. aplicación *x* que trabaja con ODBC 3. el controlador *x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** con el mismo resultado, ODBC 3. el controlador *x* debe devolver SQL_NO_DATA.
