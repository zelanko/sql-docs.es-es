---
description: Cumplimiento de JDBC 4.3 con el controlador JDBC
title: Cumplimiento de JDBC 4.3 con el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4ce01ec71649549166aa6a3d2f33d9dbb157e08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438357"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Cumplimiento de JDBC 4.3 con el controlador JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Las versiones anteriores de Microsoft JDBC Driver 6.4 para SQL Server solo son compatibles con las especificaciones de la API de Java Database Connectivity (JDBC) 4.2. Esta sección no es aplicable a la versión 6.4 ni a versiones anteriores.

A partir de la versión 6.4, Microsoft JDBC Driver para SQL Server es compatible con JAVA 9 e inicia `SQLFeatureNotSupportedException` para nuevas API de JDBC 4.3 con métodos no implementados.

Con la versión 7.0 de Microsoft JDBC Driver para SQL Server, el controlador ahora es compatible con JAVA 10 y admite las API mencionadas a continuación. El controlador inicia `SQLFeatureNotSupportedException` para otros métodos no implementados de las especificaciones de JDBC 4.3.

|Nueva API|Descripción|Implementación importante|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|Sugiere al controlador que una solicitud, una unidad de trabajo independiente, se inicia en esta conexión. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Guarda los valores de los campos de conexión que se pueden modificar a través de métodos de la API pública: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|Sugiere al controlador que una solicitud, una unidad de trabajo independiente, se ha completado. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Cierra las instrucciones que se crean durante la unidad de trabajo y revierte cualquier transacción abierta. El método también revierte los cambios en los campos de conexión que se muestran arriba.|
