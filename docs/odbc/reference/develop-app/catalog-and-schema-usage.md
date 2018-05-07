---
title: Uso de esquema y catálogo | Documentos de Microsoft
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0aa8e5c112bbd3bc807ecba821da2e754016b23a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-and-schema-usage"></a>Uso de esquema y catálogo
Orígenes de datos no admiten necesariamente los nombres de catálogo y el esquema como identificadores de nombre de objeto en todas las instrucciones SQL. Orígenes de datos podrían admitir nombres de catálogo y el esquema en una o varias de las siguientes clases de instrucciones SQL: instrucciones de lenguaje de manipulación de datos (DML), llamadas a procedimiento, instrucciones de definición de tabla, las instrucciones de definición de índice y definición de privilegios instrucciones. Para determinar las clases de instrucciones SQL en las que catálogo y esquema de nombres se pueden usar, llama a una aplicación **SQLGetInfo** con las opciones SQL_CATALOG_USAGE y SQL_SCHEMA_USAGE.
