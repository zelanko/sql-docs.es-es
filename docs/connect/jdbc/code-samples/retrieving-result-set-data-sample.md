---
title: Recuperando ejemplo de datos del conjunto de resultados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cca84ebc59bdefb43e2aa1a5f8b62bbf6301d51
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028371"
---
# <a name="retrieving-result-set-data-sample"></a>Recuperación de ejemplo de datos de conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] muestra cómo recuperar un conjunto de datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y luego cómo mostrar esos datos.

El archivo de código para este ejemplo se llama RetrieveResultSet.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets  
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de clases, vea [usar el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información sobre el archivo JAR que se debe seleccionar, vea [Requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código de ejemplo realiza una conexión a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Luego, mediante una instrucción SQL con el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), ejecuta la instrucción SQL y coloca los datos devueltos en un objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).

Después, el código de ejemplo llama al método displayRow personalizado para recorrer en iteración las filas de datos que están en el conjunto de resultados y usa el método [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) para mostrar algunos de los datos.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class RetrieveRS {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            createTable(stmt);
        String SQL = "SELECT * FROM Production.Product;";
            ResultSet rs = stmt.executeQuery(SQL);
            displayRow("PRODUCTS", rs);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void displayRow(String title,
            ResultSet rs) throws SQLException {
        System.out.println(title);
        while (rs.next()) {
            System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));
        }
    }

    private static void createTable(Statement stmt) throws SQLException {
        stmt.execute("if exists (select * from sys.objects where name = 'Product_JDBC_Sample')"
                + "drop table Product_JDBC_Sample");

        String sql = "CREATE TABLE [Product_JDBC_Sample](" + "[ProductID] [int] IDENTITY(1,1) NOT NULL,"
                + "[Name] [varchar](30) NOT NULL," + "[ProductNumber] [nvarchar](25) NOT NULL,"
                + "[MakeFlag] [bit] NOT NULL," + "[FinishedGoodsFlag] [bit] NOT NULL," + "[Color] [nvarchar](15) NULL,"
                + "[SafetyStockLevel] [smallint] NOT NULL," + "[ReorderPoint] [smallint] NOT NULL,"
                + "[StandardCost] [money] NOT NULL," + "[ListPrice] [money] NOT NULL," + "[Size] [nvarchar](5) NULL,"
                + "[SizeUnitMeasureCode] [nchar](3) NULL," + "[WeightUnitMeasureCode] [nchar](3) NULL,"
                + "[Weight] [decimal](8, 2) NULL," + "[DaysToManufacture] [int] NOT NULL,"
                + "[ProductLine] [nchar](2) NULL," + "[Class] [nchar](2) NULL," + "[Style] [nchar](2) NULL,"
                + "[ProductSubcategoryID] [int] NULL," + "[ProductModelID] [int] NULL,"
                + "[SellStartDate] [datetime] NOT NULL," + "[SellEndDate] [datetime] NULL,"
                + "[DiscontinuedDate] [datetime] NULL," + "[rowguid] [uniqueidentifier] ROWGUIDCOL  NOT NULL,"
                + "[ModifiedDate] [datetime] NOT NULL,)";

        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('Adjustable Time','AR-5381','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('ML Bottom Bracket','BB-8107','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);

        sql = "INSERT Product_JDBC_Sample VALUES ('Mountain-500 Black, 44','BK-M18B-44','0','0',NULL,'1000','750','0.00','0.00',NULL,NULL,NULL,NULL,'0',NULL,NULL,NULL,NULL,NULL,'2008-04-30 00:00:00.000',NULL,NULL,'694215B7-08F7-4C0D-ACB1-D734BA44C0C8','2014-02-08 10:01:36.827') ";
        stmt.execute(sql);
    }

    private static void displayRow(String title, ResultSet rs) {
        try {
            System.out.println(title);
            while (rs.next()) {
                System.out.println(rs.getString("ProductNumber") + " : " + rs.getString("Name"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

## <a name="see-also"></a>Vea también

[Trabajo con conjuntos de resultados](../../../connect/jdbc/code-samples/working-with-result-sets.md)
