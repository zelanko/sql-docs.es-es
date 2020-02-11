---
title: Múltiples instrucciones y conexiones activas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76b74ff748a62a401955e4ea4a995f507314124e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942824"
---
# <a name="multiple-active-statements-and-connections"></a>Varias instrucciones activas y las conexiones
Algunos controladores y DBMS limitan el número de instrucciones y conexiones que pueden estar activas al mismo tiempo. Estos números pueden ser tan pequeños como uno. Para obtener más información, vea las opciones SQL_MAX_CONCURRENT_ACTIVITIES y SQL_MAX_DRIVER_CONNECTIONS en la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) , y los [identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md) y de la [conexión](../../../odbc/reference/develop-app/connection-handles.md).
