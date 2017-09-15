---
title: Cumplimiento de la interfaz de nivel 2 | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c272637e15d95a09862170ec871274adb624c271
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="level-2-interface-conformance"></a>Cumplimiento de la interfaz de nivel 2
El nivel de conformidad de interfaz de nivel 2 incluye la funcionalidad de conformidad: nivel de interfaz de nivel 1 y las características siguientes:  
  
|||  
|-|-|  
|201|Usar nombres de tres partes de tablas de base de datos y vistas. (Para obtener más información, consulte la dos partes nomenclatura característica Compatibilidad con 101 en [cumplimiento a nivel 1 interfaz](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Se describen los parámetros dinámicos, mediante una llamada a **SQLDescribeParam**.|  
|203|Utilice no solo parámetros de entrada, pero también parámetros de entrada/salida y salidos y valores de resultado de los procedimientos almacenados.|  
|204|Utilizar marcadores, incluidos los marcadores, la recuperación mediante una llamada a **SQLDescribeCol** y **SQLColAttribute** en la columna número 0; de filas basado en un marcador, mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento establecido en SQL_FETCH_BOOKMARK; y la actualización, eliminar y capturar las operaciones de marcador, mediante una llamada a **SQLBulkOperations** con el *Operación* establecido en SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperar información avanzada sobre el diccionario de datos, mediante una llamada a **SQLColumnPrivileges**, **SQLForeignKeys**, y **SQLTablePrivileges**.|  
|206|Usar funciones ODBC en lugar de instrucciones SQL para realizar operaciones de base de datos adicional, mediante una llamada a **SQLBulkOperations** con SQL_ADD, o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. (Soporte técnico para las llamadas a **SQLSetPos** con el *LockType* argumento establecido en SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK no es una parte de los niveles de cumplimiento, pero es una característica opcional.)|  
|207|Habilitar la ejecución asincrónica de funciones ODBC para las instrucciones individuales especificadas.|  
|208|Obtener la columna SQL_ROWVER de identificación de filas de tablas, mediante una llamada a **SQLSpecialColumns**. (Para obtener más información, vea la compatibilidad con **SQLSpecialColumns** con el *IdentifierType* establecido en SQL_BEST_ROWID como característica 20 en [Core interfaz conformidad](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|Establezca el atributo de instrucción SQL_ATTR_CONCURRENCY en al menos un valor distinto de SQL_CONCUR_READ_ONLY.|  
|210|La capacidad de solicitud de inicio de sesión de tiempo de espera y las consultas SQL (SQL_ATTR_LOGIN_TIMEOUT y SQL_ATTR_QUERY_TIMEOUT).|  
|211|La capacidad de cambiar el nivel de aislamiento predeterminado; la capacidad de ejecutar las transacciones con el nivel de aislamiento "serializable".|
