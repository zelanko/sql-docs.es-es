---
title: Descripción de las transacciones | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6045c482a931329e3d62c49dedea7ea86a14c545
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-transactions"></a>Descripción de transacciones
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Las transacciones son grupos de operaciones que se combinan en unidades lógicas de trabajo. Se usan para controlar y mantener la coherencia y la integridad de cada acción de una transacción, a pesar de los errores que puedan producirse en el sistema,  
  
 Con el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], las transacciones pueden ser local o distribuida. Las transacciones también pueden usar niveles de aislamiento. Para obtener más información acerca de los niveles de aislamiento admitidos por el controlador JDBC, consulte [niveles de aislamiento de descripción](../../connect/jdbc/understanding-isolation-levels.md).  
  
 LAs aplicaciones deben controlar las transacciones usando las instrucciones Transact-SQ o los métodos proporcionados por el controlador JDBC, pero no ambos. Usar en la misma transacción las instrucciones Transact-SQL y los métodos API de JDBC podría producir problemas, como que una transacción no pueda ser confirmada cuando se espera, que la transacción sea confirmada o se revierta y se inicie una nueva inesperadamente, o las excepciones "No se pudo reanudar la transacción".  
  
## <a name="using-local-transactions"></a>Usar transacciones locales  
 Se considera que una transacción es local cuando es de una sola fase y la base de datos la trata directamente. El controlador JDBC admite las transacciones locales mediante el uso de varios métodos de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) de la clase, incluidos los [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [confirmación](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)y [reversión](../../connect/jdbc/reference/rollback-method.md). Las transacciones locales suelen ser administradas explícitamente por la aplicación o automáticamente por el servidor de aplicaciones de Java Platform, Enterprise Edition (Java EE).  
  
 En el ejemplo siguiente se realiza una transacción local que consta de dos instrucciones independientes en el `try` bloque. Las instrucciones se ejecutan en la tabla Production.ScrapReason en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo y se confirman si no se produce ninguna excepción. El código en el `catch` bloque revierte la transacción si se produce una excepción.  
  
 [!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]  
  
## <a name="using-distributed-transactions"></a>Usar transacciones distribuidas  
 Una transacción distribuida es una transacción que actualiza datos en dos o más bases de datos conectadas a una red manteniendo las propiedades atómicas, coherentes, aisladas y durables (ACID) del procesamiento de la transacción. La compatibilidad con las transacciones distribuidas se incluyó en la API de JDBC de la especificación API Opcional de JDBC 2.0. La administración de transacciones distribuidas normalmente se realiza de forma automática por parte del administrador de transacciones Servicio de Transacciones de Java (JTS) dentro de un entorno de servidor de aplicaciones Java EE. Sin embargo, la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite transacciones distribuidas en cualquier administrador de transacciones compatible con API de transacciones de Java (JTA).  
  
 El controlador JDBC se integra perfectamente con [!INCLUDE[msCoName](../../includes/msconame_md.md)] Coordinador de transacciones distribuidas (MS DTC) para proporcionar true distribuidas compatibilidad con transacciones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. MS DTC es una herramienta de transacciones distribuidas proporcionada por [!INCLUDE[msCoName](../../includes/msconame_md.md)] para [!INCLUDE[msCoName](../../includes/msconame_md.md)] sistemas Windows. MS DTC usa tecnología de procesamiento de transacciones de eficacia comprobada de [!INCLUDE[msCoName](../../includes/msconame_md.md)] para admitir características XA tales como el protocolo de confirmación distribuida en dos fases completo y la recuperación de transacciones distribuidas.  
  
 Para obtener más información acerca de cómo utilizar las transacciones distribuidas, consulte [descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Vea también  
 [Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
