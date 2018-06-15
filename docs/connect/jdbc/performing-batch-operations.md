---
title: Realizar operaciones por lotes | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55470e4246256f2dfce11464ab8aafb9c9e7873c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32831870"
---
# <a name="performing-batch-operations"></a>Realizar operaciones por lotes
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para mejorar el rendimiento al realizar varias actualizaciones para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos se producen, el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ofrece la posibilidad de enviar varias actualizaciones como una sola unidad de trabajo, también denominada como un lote.  
  
 El [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clases pueden utilizarse para enviar actualizaciones por lotes. El [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) método se utiliza para agregar un comando. El [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) método se usa para borrar la lista de comandos. El [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) método se usa para enviar todos los comandos para su procesamiento. Tan solo las instrucciones de lenguaje de definición de datos (DDL) y lenguaje de manipulación de datos (DML) que devuelven un recuento de actualizaciones sencillo se pueden ejecutar como parte de un lote.  
  
 El método executeBatch devuelve una matriz de **int** valores que se corresponden con el número de actualizaciones de cada comando. Si se produce un error en uno de los comandos, se produce un BatchUpdateException y debe usar el método getUpdateCounts de la clase BatchUpdateException para recuperar la matriz de recuento de actualizaciones. Si un comando produce un error, el controlador sigue procesando los comandos restantes. No obstante, si un comando contiene un error de sintaxis, las instrucciones del lote generan un error.  
  
> [!NOTE]  
>  Si no tiene que usar recuentos de actualizaciones, primero puede emitir una instrucción SET NOCOUNT ON para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. De este modo, se reduce el tráfico de red y, además, se aumenta el rendimiento de la aplicación.  
  
 Por ejemplo, cree la siguiente tabla en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo:  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 En el ejemplo siguiente, una conexión abierta a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo se pasa a la función, el método addBatch se usa para crear las instrucciones que se ejecutará y se llama al método executeBatch para enviar el lote a la base de datos.  
  
```  
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
  
## <a name="see-also"></a>Vea también  
 [Usar instrucciones con el controlador JDBC](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
