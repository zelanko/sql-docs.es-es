---
title: JDBC 4.3 cumplimiento para el controlador JDBC | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 02aef28bb40c4d4f48b28630d1752c9e5f88c3e5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781550"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Cumplimiento de JDBC 4.3 con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Las versiones anteriores de Microsoft JDBC Driver 6.4 para SQL Server solo son compatibles con las especificaciones de la API de Java Database Connectivity (JDBC) 4.2. Esta sección no es aplicable a la versión 6.4 ni a versiones anteriores.

A partir de la versión 6.4, Microsoft JDBC Driver para SQL Server es compatible con JAVA 9 y produce `SQLFeatureNotSupportedException` para nuevas JDBC 4.3 API que han sin implementar métodos.

Con Microsoft JDBC Driver 7.0 para la versión de SQL Server, el controlador ahora es 10 compatible de JAVA, y admite siguiente mencionados API. El controlador lanzará `SQLFeatureNotSupportedException` para otros métodos de las especificaciones de JDBC 4.3 no implementadas.

|Nueva API|Descripción|Implementación importante|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Sugerencias para el controlador que se está iniciando una solicitud, una unidad independiente de trabajo, en esta conexión. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Guarda los valores de los campos de conexión son modificables a través de métodos de la API públicos: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Sugerencias para el controlador que se ha completado una solicitud, una unidad de trabajo independiente. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Las instrucciones que se crean durante la unidad de trabajo se cierra y revierte cualquier transacción abierta. El método también revierte los cambios realizados en los campos de conexión que se indican a continuación.|
