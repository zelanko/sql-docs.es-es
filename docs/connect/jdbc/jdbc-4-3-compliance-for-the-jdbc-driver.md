---
title: JDBC 4.3 cumplimiento para el controlador JDBC | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f529c88044444f3fb6e428b6c69f5a5cf5917251
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278916"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>Cumplimiento de JDBC 4.3 con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Las versiones anteriores de Microsoft JDBC Driver 6.4 para SQL Server son compatibles con las especificaciones de la API de Java Database Connectivity (JDBC) 4.2. Esta sección no es aplicable a las versiones anteriores a la versión 6.4.  
  
 A partir de la versión 6.4, Microsoft JDBC Driver para SQL Server es compatible con 10 JAVA, pero no es totalmente compatible con las especificaciones de JDBC 4.3 de API. El controlador lanzará SQLFeatureNotSupportedException para métodos no está implementados. 
 
 Los siguientes métodos de API de JDBC 4.3 se implementan en Microsoft JDBC Driver 6.4 para SQL Server.
 
  **Clase SQLServerConnection**  
  
|Nuevos métodos|Descripción|Implementación importante|  
|-----------------|-----------------|-------------------------------|  
|void beginRequest()|Sugerencias para el controlador que se está iniciando una solicitud, una unidad independiente de trabajo, en esta conexión. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--).|Guarda los valores de los campos de conexión son modificables a través de métodos de la API públicos: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall `, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void endRequest()|Sugerencias para el controlador que se ha completado una solicitud, una unidad de trabajo independiente. Para más información, vea [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--).|Las instrucciones que se crean durante la unidad de trabajo se cierra y revierte cualquier transacción abierta. El método también revierte los cambios realizados en los campos de conexión que se indican a continuación.|