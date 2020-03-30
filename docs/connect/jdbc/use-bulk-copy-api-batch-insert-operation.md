---
title: Uso de la API de copia masiva para la operación de inserción por lotes para el controlador JDBC de MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027105"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Uso de la API de copia masiva para la operación de inserción por lotes

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 para SQL Server admite el uso de la API de copia masiva para las operaciones de inserción por lotes para Azure Data Warehouse. Esta característica permite a los usuarios habilitar el controlador para realizar la siguiente operación de copia masiva al ejecutar las operaciones de inserción por lotes. El objetivo del controlador es lograr que mejore el rendimiento mientras se insertan los mismos datos que tendría el controlador con la operación de inserción por lotes normal. El controlador analiza la consulta SQL del usuario, aprovechando la API de copia masiva en lugar de la operación de inserción por lotes normal. A continuación se muestran varias formas de habilitar la API de copia masiva para la característica de inserción por lotes, así como la lista de sus limitaciones. En esta página también se incluye un pequeño código de ejemplo que muestra un uso, además del aumento del rendimiento.

Esta característica solo es aplicable a las API `executeBatch()` & `executeLargeBatch()` de PreparedStatement y CallableStatement.

## <a name="prerequisites"></a>Prerrequisitos

Hay dos requisitos previos para habilitar la API de copia masiva para la inserción por lotes.

* El servidor debe ser Azure Data Warehouse.
* La consulta debe ser una consulta insert (la consulta puede contener comentarios, pero debe empezar por la palabra clave INSERT para que esta característica surta efecto).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Habilitación de la API de copia masiva para la inserción por lotes

Hay tres formas de habilitar la API de copia masiva para la inserción por lotes.

### <a name="1-enabling-with-connection-property"></a>1. Habilitación con la propiedad de conexión

La incorporación de **useBulkCopyForBatchInsert=true;** a la cadena de conexión habilita esta característica.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Habilitación con el método setUseBulkCopyForBatchInsert() del objeto SQLServerConnection

La llamada a **SQLServerConnection.setUseBulkCopyForBatchInsert(true)** habilita esta característica.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** recupera el valor actual para la propiedad de conexión **useBulkCopyForBatchInsert**.

El valor de **useBulkCopyForBatchInsert** sigue siendo constante para cada PreparedStatement en el momento de su inicialización. Ninguna llamada subsiguiente a **SQLServerConnection.setUseBulkCopyForBatchInsert()** afectará a la instrucción PreparedStatement ya creada con respecto a su valor.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Habilitación con el método setUseBulkCopyForBatchInsert() del objeto SQLServerDataSource

Similar al anterior, pero se usa SQLServerDataSource para crear un objeto SQLServerConnection. Con ambos métodos se obtiene el mismo resultado.

## <a name="known-limitations"></a>Restricciones conocidas

Actualmente existen estas limitaciones que se aplican a esta característica.

* Las consultas insert con valores sin parámetros (por ejemplo, `INSERT INTO TABLE VALUES (?, 2`), no se admiten. Los caracteres comodín (?) son los únicos caracteres admitidos para esta función.
* Las consultas insert con expresiones INSERT-SELECT (por ejemplo, `INSERT INTO TABLE SELECT * FROM TABLE2`) no se admiten.
* Las consultas insert con varias expresiones VALUE (por ejemplo, `INSERT INTO TABLE VALUES (1, 2) (3, 4)`) no se admiten.
* Las consultas insert a las que sigue la cláusula OPTION, unidas con varias tablas o seguidas de otra consulta, no se admiten.
* Debido a las limitaciones de la API de copia masiva, los tipos de datos `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY` y `GEOGRAPHY` no se admiten actualmente para esta característica.

Si se produce un error en la consulta por errores no relacionados con "SQL Server", el controlador registrará el mensaje de error y retrocederá a la lógica original para la inserción por lotes.

## <a name="example"></a>Ejemplo

A continuación aparece un código de ejemplo que muestra el caso de uso para una operación de inserción por lotes en Azure DW de mil filas, para ambos escenarios (normal frente a API de copia masiva).

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

[Mejora del rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
