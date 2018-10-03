---
title: Cumplimiento de la interfaz de nivel 2 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f3828129c2a0ed4183bbefce8daf68cee1d95f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668303"
---
# <a name="level-2-interface-conformance"></a>Cumplimiento de la interfaz de nivel 2
El nivel de conformidad de interfaz de nivel 2 incluye la funcionalidad de nivel 1 interfaz: el nivel de cumplimiento y las características siguientes:  
  
|||  
|-|-|  
|201|Usar nombres de tres partes de las tablas de base de datos y vistas. (Para obtener más información, vea la dos partes nomenclatura soporte característica 101 en [cumplimiento de la interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Describir los parámetros dinámicos mediante una llamada a **SQLDescribeParam**.|  
|203|Usar no solo los parámetros de entrada, pero también los parámetros de salida y entrada/salida y valores de resultado de los procedimientos almacenados.|  
|204|Uso de marcadores, como el de recuperación marcadores, mediante una llamada a **SQLDescribeCol** y **SQLColAttribute** en la columna número 0; capturando basado en un marcador, mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento establecido en SQL_FETCH_BOOKMARK; y actualizar, eliminar y capturar las operaciones de marcador, mediante una llamada a **SQLBulkOperations** con el *Operación* establecido en SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK o SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperar información avanzada sobre el diccionario de datos, mediante una llamada a **SQLColumnPrivileges**, **SQLForeignKeys**, y **SQLTablePrivileges**.|  
|206|Usar funciones de ODBC en lugar de instrucciones SQL para realizar operaciones de base de datos adicional, mediante una llamada a **SQLBulkOperations** con SQL_ADD, o **SQLSetPos** con SQL_DELETE o SQL_UPDATE. (Soporte técnico para las llamadas a **SQLSetPos** con el *LockType* argumento establecido en SQL_LOCK_EXCLUSIVE o SQL_LOCK_UNLOCK no forma parte de los niveles de compatibilidad, pero es una característica opcional.)|  
|207|Habilitar la ejecución asincrónica de funciones ODBC para instrucciones individuales especificadas.|  
|208|Obtener la columna que identifica la fila SQL_ROWVER de tablas, mediante una llamada a **SQLSpecialColumns**. (Para obtener más información, consulte la compatibilidad con **SQLSpecialColumns** con el *IdentifierType* establecido en SQL_BEST_ROWID como característica 20 en [cumplimiento de la interfaz Core](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|Establezca el atributo de instrucción SQL_ATTR_CONCURRENCY en al menos un valor distinto de SQL_CONCUR_READ_ONLY.|  
|210|La capacidad de solicitud de inicio de sesión de tiempo de espera y las consultas SQL (SQL_ATTR_LOGIN_TIMEOUT y SQL_ATTR_QUERY_TIMEOUT).|  
|211|La capacidad de cambiar el nivel de aislamiento predeterminado; la capacidad para ejecutar transacciones con el nivel de aislamiento "serializable".|
