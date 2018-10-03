---
title: Varias instrucciones activas y conexiones | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b2a1edbf9947aff01ef6d4688959352986cf672d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745723"
---
# <a name="multiple-active-statements-and-connections"></a>Varias instrucciones activas y las conexiones
Algunos controladores y DBMS limitan el número de instrucciones y las conexiones que pueden estar activas al mismo tiempo. Estos números pueden ser tan pequeños como uno. Para obtener más información, vea las opciones SQL_MAX_CONCURRENT_ACTIVITIES y SQL_MAX_DRIVER_CONNECTIONS en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción, de la función y [instrucción controla](../../../odbc/reference/develop-app/statement-handles.md) y [ Identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md).
