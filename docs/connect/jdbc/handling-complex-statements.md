---
title: Controlar instrucciones complejas | Documentos de Microsoft
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
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7eb061374707182a9ccc2cd26e223387c580d72a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="handling-complex-statements"></a>Controlar instrucciones complejas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], puede que tenga que controlar instrucciones complejas, incluidas instrucciones generadas dinámicamente en tiempo de ejecución. Las instrucciones complejas suelen realizar tareas diversas como actualizaciones, inserciones y eliminaciones. Estos tipos de instrucciones pueden devolver varios conjuntos de resultados y parámetros de salida. En estos casos, el código Java que ejecuta las instrucciones puede no saber por anticipado los tipos y el número de objetos y datos devueltos.  
  
 Para procesar las instrucciones complejas del modo adecuado, el controlador JDBC proporciona una serie de métodos para consultar los objetos y datos devueltos para que la aplicación pueda procesarlos correctamente. La clave para procesar las instrucciones complejas es el [ejecutar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase. Este método devuelve un **booleano** valor. Si el valor es true, el primer resultado devuelto de las instrucciones es un conjunto de resultados. Si el valor es false, el primer resultado devuelto es un recuento de actualizaciones.  
  
 Si conoce el tipo de objeto o datos devueltos, puede usar el [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) o [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) método para procesar los datos. Para continuar con el siguiente objeto o datos que se devuelven desde la instrucción compleja, puede llamar a la [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) método.  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, se genera una instrucción compleja que combina una llamada de procedimiento almacenado con una instrucción SQL, las instrucciones se ejecutan y, a continuación, un `do` bucle es se usa para procesar todos los conjuntos de lo resultados y recuentos se devuelven de actualizaciones.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
