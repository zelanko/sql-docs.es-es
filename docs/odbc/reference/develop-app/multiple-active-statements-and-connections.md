---
title: Múltiples declaraciones activas y conexiones ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], multiple active statements and connections
- multiple active statements and connections [ODBC]
ms.assetid: a6571356-b23e-4f10-a17b-bce09460b71e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8259967942f47b06c50a9043158f8b3b45c58d7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302434"
---
# <a name="multiple-active-statements-and-connections"></a>Varias instrucciones activas y las conexiones
Algunos controladores y DBMS limitan el número de instrucciones y conexiones que pueden estar activas a la vez. Estos números pueden ser tan pequeños como uno. Para obtener más información, vea las opciones SQL_MAX_CONCURRENT_ACTIVITIES y SQL_MAX_DRIVER_CONNECTIONS en la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y Identificadores de [instrucción](../../../odbc/reference/develop-app/statement-handles.md) y [identificadores](../../../odbc/reference/develop-app/connection-handles.md)de conexión .
