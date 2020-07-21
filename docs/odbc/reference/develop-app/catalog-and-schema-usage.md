---
title: Uso de catálogos y esquemas | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306256"
---
# <a name="catalog-and-schema-usage"></a>Uso de esquema y catálogo
Los orígenes de datos no admiten necesariamente nombres de catálogo y de esquema como identificadores de nombre de objeto en todas las instrucciones SQL. Los orígenes de datos pueden admitir nombres de catálogo y de esquema en una o varias de las siguientes clases de instrucciones SQL: instrucciones del lenguaje de manipulación de datos (DML), llamadas a procedimientos, instrucciones de definición de tabla, instrucciones de definición de índices e instrucciones de definición de privilegios. Para determinar las clases de instrucciones SQL en las que se pueden usar nombres de esquema y de catálogo, una aplicación llama a **SQLGetInfo** con las opciones SQL_CATALOG_USAGE y SQL_SCHEMA_USAGE.
