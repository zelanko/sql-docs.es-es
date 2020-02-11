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
ms.openlocfilehash: 1f899e7a034e1ec5fc967d834caad3a4ccc4caa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041832"
---
# <a name="sql_no_data"></a>SQL_NO_DATA
Cuando se trata de un ODBC 3. la aplicación *x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** en ODBC 2. controlador *x* para ejecutar una instrucción UPDATE o DELETE buscada que no afecte a ninguna fila del origen de datos, el controlador debe devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando se trata de un ODBC 2. *x* o ODBC 3. aplicación *x* que trabaja con ODBC 3. el controlador *x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** con el mismo resultado, ODBC 3. el controlador *x* debe devolver SQL_NO_DATA.
