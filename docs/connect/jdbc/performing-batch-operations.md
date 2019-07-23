---
title: Realización de operaciones por lotes | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 244c20b2fb7721d117557581068791e1a2d99d14
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956226"
---
# <a name="performing-batch-operations"></a>Realizar operaciones por lotes
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Con el fin de aumentar el rendimiento al realizar varias actualizaciones en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ofrece la posibilidad de enviar varias actualizaciones como una sola unidad de trabajo, denominada también lote.  
  
 Las clases [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) se pueden usar para enviar actualizaciones por lotes. El método [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) se usa para agregar un comando. El método [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) se usa para borrar la lista de comandos. El método [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) se usa para enviar todos los comandos para su procesamiento. Tan solo las instrucciones de lenguaje de definición de datos (DDL) y lenguaje de manipulación de datos (DML) que devuelven un recuento de actualizaciones sencillo se pueden ejecutar como parte de un lote.  
  
 El método executeBatch devuelve una matriz de valores **int** que se corresponde con el recuento de actualizaciones de cada comando. Si se produce un error en uno de los comandos, se produce una BatchUpdateException y debe usar el método getUpdateCounts de la clase BatchUpdateException para recuperar la matriz de recuento de actualizaciones. Si un comando produce un error, el controlador sigue procesando los comandos restantes. No obstante, si un comando contiene un error de sintaxis, las instrucciones del lote generan un error.  
  
> [!NOTE]  
>  Si no necesita usar recuentos de actualizaciones, puede ejecutar primero la instrucción SET NOCOUNT ON para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De este modo, se reduce el tráfico de red y, además, se aumenta el rendimiento de la aplicación.  
  
 A modo de ejemplo, cree la siguiente tabla en la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 En el siguiente ejemplo, se pasa una conexión abierta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] a la función, se usa el método addBatch para crear las instrucciones que se van a ejecutar y se llama al método executeBatch para enviar el lote a la base de datos.  
  
```java
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
