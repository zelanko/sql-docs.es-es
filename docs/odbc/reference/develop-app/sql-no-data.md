---
title: SQL_NO_DATA | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- application upgrades [ODBC], SQL_NO_DATA
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
- upgrading applications [ODBC], SQL_NO_DATA
ms.assetid: 07a4144a-a548-4578-b2be-715c3cf73bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff7ba5184642f419a62ffef0610bfc08995ed6b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911220"
---
# <a name="sqlnodata"></a>SQL_NO_DATA
Cuando un ODBC 3. *x* aplicación llama **SQLExecDirect**, **SQLExecute**, o **SQLParamData** en una API ODBC 2. *x* controlador para ejecutar una actualización por búsqueda o delete, instrucción que no afecta a las filas del origen de datos, el controlador debería devolver SQL_SUCCESS, no SQL_NO_DATA. Cuando un ODBC 2. *x* u ODBC 3. *x* aplicación trabajar con una aplicación ODBC 3. *x* controlador llama **SQLExecDirect**, **SQLExecute**, o **SQLParamData** con el mismo resultado, ODBC 3. *x* controlador debería devolver SQL_NO_DATA.
