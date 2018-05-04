---
title: Usar puntos de retorno | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d7b02dfda385b0a5a8f5f7c1c8de710dade69b7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-savepoints"></a>Usar puntos de retorno
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Los puntos de retorno ofrecen un mecanismo para revertir partes de una transacción. Dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede crear un punto de retorno mediante la instrucción SAVE TRANSACTION savepoint_name. Más adelante, ejecute una instrucción ROLLBACK TRANSACTION savepoint_name para revertir al punto de retorno en vez de revertir al inicio de la transacción.  
  
 Los puntos de retorno son útiles en situaciones en que no es probable que se produzcan errores. El uso de un punto de retorno para revertir parte de una transacción, en caso de producirse un error no frecuente, puede resultar más eficaz que hacer que cada transacción pruebe si una actualización es válida antes de realizarla. Las operaciones de actualización y reversión son costosas, por lo que los puntos de retorno solamente son eficaces si la probabilidad de encontrar un error es baja y el costo de comprobar de antemano la validez de una actualización es relativamente alto.  
  
 El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el uso de puntos de retorno a través de la [setSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. Al usar el método setSavepoint, puede crear un punto de retorno con o sin nombre dentro de la transacción actual, y el método devolverá un [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto. Se pueden crear varios puntos de retorno en una transacción. Para revertir una transacción a un punto de retorno determinado, puede pasar el objeto SQLServerSavepoint a la [rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) método.  
  
 En el ejemplo siguiente, se utiliza un punto de retorno al realizar una transacción local consistente en dos instrucciones independientes en el `try` bloque. Las instrucciones se ejecutan en la tabla Production.ScrapReason en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] se utiliza la base de datos de ejemplo y un punto de retorno para revertir la segunda instrucción. Como resultado, solo se confirma en la base de datos la primera instrucción.  
  
 [!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
