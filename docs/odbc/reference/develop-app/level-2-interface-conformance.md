---
title: Conformidad de la interfaz de nivel 2 ? Microsoft Docs
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
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306167"
---
# <a name="level-2-interface-conformance"></a>Cumplimiento de la interfaz de nivel 2
El nivel de conformidad de la interfaz de nivel 2 incluye la funcionalidad de nivel de conformidad de la interfaz de nivel 1, además de las siguientes características:  
  
|||  
|-|-|  
|201|Utilice nombres de tres partes de tablas y vistas de base de datos. (Para obtener más información, consulte la característica de compatibilidad de nomenclatura de dos partes 101 en Conformidad de [interfaz](../../../odbc/reference/develop-app/level-1-interface-conformance.md)de nivel 1 .)|  
|202|Describir parámetros dinámicos mediante una llamada a **SQLDescribeParam**.|  
|203|Utilice no sólo parámetros de entrada, sino también parámetros de salida y entrada/salida, y valores de resultado de procedimientos almacenados.|  
|204|Utilice marcadores, incluida la recuperación de marcadores, llamando a **SQLDescribeCol** y **SQLColAttribute** en el número de columna 0; obtención basada en un marcador, mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento establecido en SQL_FETCH_BOOKMARK; y actualizar, eliminar y recuperar mediante operaciones de marcador, mediante una llamada a **SQLBulkOperations** con el *Operation* argumento establecido en SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperar información avanzada sobre el diccionario de datos, llamando a **SQLColumnPrivileges**, **SQLForeignKeys**y **SQLTablePrivileges**.|  
|206|Utilice funciones ODBC en lugar de instrucciones SQL para realizar operaciones de base de datos adicionales, llamando a **SQLBulkOperations** con SQL_ADD o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. (La compatibilidad con llamadas a **SQLSetPos** con el *argumento LockType* establecido en SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK no forma parte de los niveles de conformidad, pero es una característica opcional.)|  
|207|Habilite la ejecución asincrónica de funciones ODBC para instrucciones individuales especificadas.|  
|208|Obtenga la SQL_ROWVER columna de tablas de identificación de filas, llamando a **SQLSpecialColumns**. (Para obtener más información, vea la compatibilidad con **SQLSpecialColumns** con el *IdentifierType* argumento establecido en SQL_BEST_ROWID como característica 20 en [compatibilidad de interfaz principal](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|Establezca el atributo de instrucción SQL_ATTR_CONCURRENCY en al menos un valor distinto de SQL_CONCUR_READ_ONLY.|  
|210|La capacidad de agotar el tiempo de espera de la solicitud de inicio de sesión y las consultas SQL (SQL_ATTR_LOGIN_TIMEOUT y SQL_ATTR_QUERY_TIMEOUT).|  
|211|La capacidad de cambiar el nivel de aislamiento predeterminado; la capacidad de ejecutar transacciones con el nivel de aislamiento "serializable".|
