---
description: Cumplimiento de la interfaz de nivel 2
title: Conformidad de la interfaz de nivel 2 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b7148b05d3870a7f23a51167fffeb1860c26d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476567"
---
# <a name="level-2-interface-conformance"></a>Cumplimiento de la interfaz de nivel 2
El nivel de conformidad de la interfaz de nivel 2 incluye la funcionalidad del nivel de cumplimiento de la interfaz de nivel 1 más las características siguientes:  
  
|Número de característica|Descripción|  
|-|-|  
|201|Usar nombres de tres partes de tablas y vistas de base de datos. (Para obtener más información, consulte la característica de compatibilidad de nomenclatura de dos partes 101 en el cumplimiento de la [interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)).|  
|202|Describir los parámetros dinámicos mediante una llamada a **SQLDescribeParam**.|  
|203|Use no solo los parámetros de entrada, sino también los parámetros de entrada y salida, y los valores de resultado de los procedimientos almacenados.|  
|204|Use marcadores, incluida la recuperación de marcadores, llamando a **SQLDescribeCol** y **SQLColAttribute** en la columna número 0; recuperación basada en un marcador, llamando a **SQLFetchScroll** con el argumento *FetchOrientation* establecido en SQL_FETCH_BOOKMARK; y actualice, elimine y recupere las operaciones de marcador mediante una llamada a **SQLBulkOperations** con el argumento *Operation* establecido en SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recupere información avanzada sobre el Diccionario de datos llamando a **SQLColumnPrivileges**, **SQLForeignKeys**y **SQLTablePrivileges**.|  
|206|Use funciones de ODBC en lugar de instrucciones SQL para realizar operaciones de base de datos adicionales, llamando a **SQLBulkOperations** con SQL_ADD o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. (La compatibilidad con las llamadas a **SQLSetPos** con el argumento *LockType* establecido en SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK no es una parte de los niveles de cumplimiento pero es una característica opcional).|  
|207|Habilitar la ejecución asincrónica de funciones ODBC para instrucciones individuales específicas.|  
|208|Obtenga la SQL_ROWVER columna de identificación de filas de las tablas mediante una llamada a **SQLSpecialColumns**. (Para obtener más información, consulte la compatibilidad con **SQLSpecialColumns** con el argumento *IdentifierType* establecido en SQL_BEST_ROWID como característica 20 en cumplimiento de la [interfaz principal](../../../odbc/reference/develop-app/core-interface-conformance.md)).|  
|209|Establezca el atributo de instrucción SQL_ATTR_CONCURRENCY en al menos un valor distinto de SQL_CONCUR_READ_ONLY.|  
|210|La capacidad de agotar el tiempo de espera de la solicitud de inicio de sesión y las consultas SQL (SQL_ATTR_LOGIN_TIMEOUT y SQL_ATTR_QUERY_TIMEOUT).|  
|211|La capacidad de cambiar el nivel de aislamiento predeterminado; la capacidad de ejecutar transacciones con el nivel de aislamiento "serializable".|
