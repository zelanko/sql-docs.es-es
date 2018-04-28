---
title: Con capacidad de alojamiento | Documentos de Microsoft
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
ms.topic: article
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55bea5aff6ef0e3d6e1e78b707c208f1b6d8c99c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-holdability"></a>Usar la capacidad de alojamiento
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  De forma predeterminada, un conjunto de resultados creado dentro de una transacción se mantiene abierto cuando se ha confirmado la transacción a la base de datos o se ha revertido. No obstante, en ocasiones es útil que el conjunto de resultados esté cerrado, incluso después de haber confirmado la transacción. Para ello, la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el uso del resultado de establece la capacidad de alojamiento.  
  
 Capacidad de alojamiento de conjunto de resultados puede establecerse mediante el [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. Al establecer la capacidad de alojamiento mediante el método setHoldability, el conjunto de resultados constantes de capacidad de alojamiento de ResultSet.HOLD_CURSORS_OVER_COMMIT o ResultSet.CLOSE_CURSORS_AT_COMMIT puede utilizarse.  
  
 El controlador JDBC también es compatible con la configuración de la capacidad de alojamiento cuando se crea uno de los objetos Statement. Al crear los objetos Statement que tengan sobrecargas con los parámetros de la capacidad de alojamiento de los conjuntos de resultados, la capacidad de alojamiento del objeto de instrucción debe coincidir con la capacidad de alojamiento de la sobrecarga. Cuando no coinciden, se genera una excepción. Esto se debe a que SQL Server solamente admite la capacidad de alojamiento en el nivel local.  
  
 La capacidad de alojamiento del conjunto de resultados es la capacidad de alojamiento del objeto SQLServerConnection que está asociado con el conjunto de resultados en el tiempo cuando se crea el conjunto de resultados para solo los cursores de servidor. Esto no se aplica a los cursores del lado cliente. Todos los conjuntos de resultados con cursores del lado cliente siempre tendrá el valor de capacidad de alojamiento de ResultSet.HOLD_CURSORS_OVER_COMMIT.  
  
 Para los cursores de servidor, cuando están conectados a SQL Server 2005 o versiones posteriores, la configuración de la capacidad de alojamiento solamente afecta a la de los nuevos conjuntos de resultados que todavía han de ser creados en esa conexión. Eso significa que la configuración de la capacidad de alojamiento no tiene impacto alguno sobre la capacidad de alojamiento de los conjuntos de resultados creados previamente que ya estaban abiertos en esa conexión. Con SQL Server 2000, sin embargo, configurar la capacidad de alojamiento afecta a la capacidad de alojamiento de los resultados existentes como a la de los nuevos conjuntos de resultados que todavía han de ser creados en esa conexión.  
  
 En el ejemplo siguiente, se establece la capacidad de alojamiento del conjunto de resultados mientras se realiza una transacción local consistente en dos instrucciones independientes en el `try` bloque. Las instrucciones se ejecutan en la tabla Production.ScrapReason en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. En primer lugar, el ejemplo cambia al modo de transacción manual configurando la confirmación automática en **false**. Una vez que se deshabilita el modo de confirmación automática, ninguna de las instrucciones SQL se confirmará hasta que la aplicación llame el [confirmación](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) método explícitamente. El código del bloque catch revierte la transacción si se lanza una excepción.  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
