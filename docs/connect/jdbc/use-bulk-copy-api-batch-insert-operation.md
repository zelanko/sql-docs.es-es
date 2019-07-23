---
title: Uso de la API de copia masiva para la operación de inserción por lotes para el controlador JDBC de MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 028caf1bf69c7e361ea7e4445c192c1fc1adf437
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004134"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Uso de la API de copia masiva para la operación de inserción por lotes

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC driver 7,0 for SQL Server admite el uso de la API de copia masiva para las operaciones de inserción por lotes para Azure Data Warehouse. Esta característica permite a los usuarios habilitar el controlador para realizar una operación de copia masiva bajo al ejecutar operaciones de inserción por lotes. El controlador tiene como objetivo lograr una mejora en el rendimiento mientras se insertan los mismos datos que tendría el controlador con la operación de inserción por lotes normal. El controlador analiza la consulta SQL del usuario, aprovechando la API de copia masiva en lugar de la operación de inserción por lotes habitual. A continuación se muestran varias maneras de habilitar la característica de la API de copia masiva para la inserción de batch, así como la lista de sus limitaciones. Esta página también contiene un pequeño código de ejemplo que muestra un uso y el aumento del rendimiento.

Esta característica solo es aplicable a las API de `executeBatch()`  &  `executeLargeBatch()` PreparedStatement y CallableStatement.

## <a name="pre-requisites"></a>Requisitos previos

Hay dos requisitos previos para habilitar la API de copia masiva para la inserción por lotes.

* El servidor debe ser Azure Data Warehouse.
* La consulta debe ser una consulta Insert (la consulta puede contener comentarios, pero la consulta debe comenzar con la palabra clave INSERT para que esta característica surta efecto).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Habilitación de la API de copia masiva para la inserción por lotes

Hay tres maneras de habilitar la API de copia masiva para la inserción por lotes.

### <a name="1-enabling-with-connection-property"></a>1. Habilitar con la propiedad de conexión

Agregar **useBulkCopyForBatchInsert = true;** a la cadena de conexión habilita esta característica.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Habilitar con el método setUseBulkCopyForBatchInsert () desde el objeto SQLServerConnection

Al llamar a **SQLServerConnection. setUseBulkCopyForBatchInsert (true)** se habilita esta característica.

**SQLServerConnection. getUseBulkCopyForBatchInsert ()** recupera el valor actual de la propiedad de conexión **useBulkCopyForBatchInsert** .

El valor de **useBulkCopyForBatchInsert** permanece constante para cada PreparedStatement en el momento de su inicialización. Las llamadas subsiguientes a **SQLServerConnection. setUseBulkCopyForBatchInsert ()** no afectarán a la imvista ya creada con respecto a su valor.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Habilitar con el método setUseBulkCopyForBatchInsert () desde el objeto SQLServerDataSource

Similar a la anterior, pero el uso de SQLServerDataSource para crear un objeto SQLServerConnection. Con ambos métodos se obtiene el mismo resultado.

## <a name="known-limitations"></a>Restricciones conocidas

Actualmente, existen estas limitaciones que se aplican a esta característica.

* No se admiten las consultas Insert que contengan valores sin `INSERT INTO TABLE VALUES (?, 2`parámetros (por ejemplo,)). Los caracteres comodín (?) son los únicos parámetros admitidos para esta función.
* No se admiten las consultas Insert que contengan expresiones `INSERT INTO TABLE SELECT * FROM TABLE2`Insert-Select (por ejemplo,).
* No se admiten las consultas Insert que contengan `INSERT INTO TABLE VALUES (1, 2) (3, 4)`varias expresiones de valor (por ejemplo,).
* No se admiten las consultas Insert seguidas por la cláusula OPTION, Unidas con varias tablas o seguidas por otra consulta.
* Debido a las limitaciones de la API de copia `MONEY`masiva `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET` `SMALLDATETIME`,, `TIME`, `GEOMETRY`,, `GEOGRAPHY` y los tipos de datos, actualmente no se admiten en este ofrecen.

Si se produce un error en la consulta debido a errores relacionados que no son de tipo "SQL Server", el controlador registrará el mensaje de error y la reserva a la lógica original para la inserción por lotes.

## <a name="example"></a>Ejemplo

A continuación se muestra un ejemplo de código que muestra el caso de uso de una operación de inserción por lotes en Azure DW de miles de filas, tanto en escenarios (normales de la API de copia masiva).

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

Resultado:

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>Consulte también

[Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
