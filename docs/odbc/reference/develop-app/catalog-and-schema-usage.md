---
title: Uso de esquema y catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9476f4f928890514354f97ce604f871bd8a06d11
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702833"
---
# <a name="catalog-and-schema-usage"></a>Uso de esquema y catálogo
Orígenes de datos no admiten necesariamente los nombres de catálogo y esquema como identificadores de nombre de objeto en todas las instrucciones SQL. Orígenes de datos podrían admitir los nombres de catálogo y esquema en una o varias de las siguientes clases de instrucciones SQL: lenguaje de manipulación de datos (DML) las instrucciones, las llamadas a procedimientos, instrucciones de definición de tabla, las instrucciones de definición de índice y definición de privilegios instrucciones. Para determinar las clases de instrucciones SQL en el catálogo y el esquema se pueden usar nombres, una aplicación llama a **SQLGetInfo** con las opciones SQL_CATALOG_USAGE y SQL_SCHEMA_USAGE.
