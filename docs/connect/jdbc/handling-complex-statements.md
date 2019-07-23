---
title: Administrar instrucciones complejas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7adee47147a8aad153bc323470f1711426d92350
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956545"
---
# <a name="handling-complex-statements"></a>Controlar instrucciones complejas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando se usa el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], puede que tenga que controlar instrucciones complejas, incluidas instrucciones generadas dinámicamente en tiempo de ejecución. Las instrucciones complejas suelen realizar tareas diversas como actualizaciones, inserciones y eliminaciones. Estos tipos de instrucciones pueden devolver varios conjuntos de resultados y parámetros de salida. En estos casos, el código Java que ejecuta las instrucciones puede no saber por anticipado los tipos y el número de objetos y datos devueltos.  
  
 Para procesar las instrucciones complejas del modo adecuado, el controlador JDBC proporciona una serie de métodos para consultar los objetos y datos devueltos para que la aplicación pueda procesarlos correctamente. La clave para procesar las instrucciones complejas es el método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). Este método devuelve un valor **booleano** . Si el valor es true, el primer resultado devuelto de las instrucciones es un conjunto de resultados. Si el valor es false, el primer resultado devuelto es un recuento de actualizaciones.  
  
 Cuando sepa el tipo de objeto o datos devueltos, puede usar el método [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) o [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) para procesar los datos. Para continuar con el objeto o datos siguientes devueltos desde la instrucción compleja, puede llamar al método [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md).  
  
 En el siguiente ejemplo, se pasa a la función una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)], se genera una instrucción compleja que combina una llamada al procedimiento almacenado con una instrucción SQL, se ejecutan las instrucciones y, a continuación, se usa un bucle `do` para procesar todos los conjuntos de resultados y recuentos de actualizaciones devueltos.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>Consulte también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
