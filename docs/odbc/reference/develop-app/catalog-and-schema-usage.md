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
ms.openlocfilehash: 4e10460df120451502d798376453d69d111051ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064415"
---
# <a name="catalog-and-schema-usage"></a>Uso de esquema y catálogo
Orígenes de datos no admiten necesariamente los nombres de catálogo y esquema como identificadores de nombre de objeto en todas las instrucciones SQL. Orígenes de datos podrían admitir los nombres de catálogo y esquema en una o varias de las siguientes clases de instrucciones SQL: Instrucciones de lenguaje de manipulación (DML) de datos, las llamadas a procedimientos, instrucciones de definición de tabla, las instrucciones de definición de índice y las instrucciones de definición de privilegios. Para determinar las clases de instrucciones SQL en el catálogo y el esquema se pueden usar nombres, una aplicación llama a **SQLGetInfo** con las opciones SQL_CATALOG_USAGE y SQL_SCHEMA_USAGE.
