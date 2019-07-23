---
title: Compatibilidad de JDBC 4,3 con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20cefb029a126b0a262d86a2dc0a0791959085bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956364"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Cumplimiento de JDBC 4.3 con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Las versiones anteriores de Microsoft JDBC Driver 6.4 para SQL Server solo son compatibles con las especificaciones de la API de Java Database Connectivity (JDBC) 4.2. Esta sección no es aplicable a la versión 6.4 ni a versiones anteriores.

A partir de la versión 6,4, Microsoft JDBC driver for SQL Server es compatible con Java 9 `SQLFeatureNotSupportedException` y produce una excepción para las nuevas API de JDBC 4,3 que tienen métodos no implementados.

Con Microsoft JDBC driver 7,0 para la versión de SQL Server, el controlador es ahora compatible con JAVA 10 y admite las API mencionadas a continuación. El controlador inicia `SQLFeatureNotSupportedException` para otros métodos no implementados de las especificaciones de JDBC 4,3.

|Nueva API|Descripción|Implementación importante|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Sugerencias para el controlador que una solicitud, una unidad de trabajo independiente, está empezando en esta conexión. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Guarda los valores de los campos de conexión que se pueden modificar a través de métodos `databaseAutoCommitMode`de API pública: `sendTimeAsDatetime`, `statementPoolingCacheSize` `transactionIsolationLevel`, `disableStatementPooling` `networkTimeout`, `serverPreparedStatementDiscardThreshold` `holdability`, `enablePrepareOnFirstPreparedStatementCall`,,,,, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Sugerencias para el controlador que ha completado una solicitud, una unidad de trabajo independiente. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Cierra las instrucciones que se crean durante la unidad de trabajo y revierte cualquier transacción abierta. El método también revierte los cambios en los campos de conexión enumerados anteriormente.|
