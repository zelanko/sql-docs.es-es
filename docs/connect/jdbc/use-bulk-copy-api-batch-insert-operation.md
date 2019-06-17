---
title: Mediante la API de copia masiva para la operación de inserción por lotes para el controlador JDBC de MSSQL | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 347ce28dc28016f95de2795bd2f5e491dd29e2d8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802643"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Uso de la API de copia masiva para la operación de inserción por lotes

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 para SQL Server admite el uso de API de copia masiva para las operaciones de inserción por lotes para almacén de datos de Azure. Esta característica permite a los usuarios habilitar el controlador realizar la operación de copia masiva debajo al ejecutar por lotes las operaciones de inserción. Operación de inserción de los objetivos de controlador para lograr mejoras de rendimiento al insertar los mismos datos que el controlador tendría con batch regular. El controlador analiza la consulta del usuario SQL, aprovecha la API de copia masiva en lugar de la operación de inserción por lotes habitual. A continuación se muestran varias maneras de habilitar la API de copia masiva para lote insertan función, así como la lista de sus limitaciones. Esta página también contiene un código de ejemplo pequeña que se muestra un uso y el aumento del rendimiento.

Esta característica solo es aplicable a PreparedStatement y del CallableStatement `executeBatch()`  &  `executeLargeBatch()` API.

## <a name="pre-requisites"></a>Requisitos previos

Hay dos requisitos previos para habilitar la API de copia masiva para la inserción por lotes.

* El servidor debe ser el almacén de datos de Azure.
* La consulta debe ser una consulta de inserción (la consulta puede contener comentarios, pero la consulta debe comenzar con la palabra clave de INSERCIÓN para que tenga efecto esta característica).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Habilitar la API de copia masiva para la inserción por lotes

Hay tres maneras de habilitar la API de copia masiva para la inserción por lotes.

### <a name="1-enabling-with-connection-property"></a>1. Habilitación de la propiedad de conexión

Agregar **useBulkCopyForBatchInsert = true;** a la conexión de cadena habilita esta característica.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Habilitar con el método setUseBulkCopyForBatchInsert() del objeto SQLServerConnection

Una llamada a **SQLServerConnection.setUseBulkCopyForBatchInsert(true)** habilita esta característica.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** recupera el valor actual de **useBulkCopyForBatchInsert** propiedad de conexión.

El valor de **useBulkCopyForBatchInsert** permanece constante para cada PreparedStatement en el momento de su inicialización. Las subsiguientes llamadas a **SQLServerConnection.setUseBulkCopyForBatchInsert()** no afectará a la PreparedStatement ya creada con respecto a su valor.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Habilitar con el método setUseBulkCopyForBatchInsert() del objeto SQLServerDataSource

Es similar al anterior, pero usa SQLServerDataSource para crear un objeto SQLServerConnection. Con ambos métodos se obtiene el mismo resultado.

## <a name="known-limitations"></a>Restricciones conocidas

Actualmente existen estas limitaciones que se aplican a esta característica.

* Inserte las consultas que contienen valores sin parámetros (por ejemplo, `INSERT INTO TABLE VALUES (?, 2`)), no se admiten. Los caracteres comodín (?) son los únicos parámetros admitidos para esta función.
* Inserte las consultas que contienen expresiones INSERT-SELECT (por ejemplo, `INSERT INTO TABLE SELECT * FROM TABLE2`), no se admiten.
* Inserte las consultas que contienen varias expresiones de valor (por ejemplo, `INSERT INTO TABLE VALUES (1, 2) (3, 4)`), no se admiten.
* No se admiten consultas de inserción que son seguidas por la cláusula OPTION, combinadas con varias tablas o seguidas de otra consulta.
* Debido a las limitaciones de API de copia masiva, `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY`, y `GEOGRAPHY` tipos de datos, no se admiten para esta característica.

Si se produce un error en la consulta debido a que no son errores relacionados con "SQL server", el controlador registrará el mensaje de error y de respaldo en la lógica de inserción por lotes original.

## <a name="example"></a>Ejemplo

A continuación es un código de ejemplo que muestra el caso de uso para una operación por lotes insert en el almacenamiento de datos de Azure de mil filas, en ambos casos (API de copia masiva de vs regulares).

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
