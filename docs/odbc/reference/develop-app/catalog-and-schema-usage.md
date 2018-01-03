---
title: "Uso de esquema y catálogo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6653d44ad75fb9e2d1941a6d280ba0ec91dd275d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="catalog-and-schema-usage"></a>Uso de esquema y catálogo
Orígenes de datos no admiten necesariamente los nombres de catálogo y el esquema como identificadores de nombre de objeto en todas las instrucciones SQL. Orígenes de datos podrían admitir nombres de catálogo y el esquema en una o varias de las siguientes clases de instrucciones SQL: instrucciones de lenguaje de manipulación de datos (DML), llamadas a procedimiento, instrucciones de definición de tabla, las instrucciones de definición de índice y definición de privilegios instrucciones. Para determinar las clases de instrucciones SQL en las que catálogo y esquema de nombres se pueden usar, llama a una aplicación **SQLGetInfo** con las opciones SQL_CATALOG_USAGE y SQL_SCHEMA_USAGE.
