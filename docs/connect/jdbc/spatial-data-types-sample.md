---
title: Ejemplo de tipos de datos espaciales para el controlador JDBC de MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a92320dc854a31384df87806bf4eca4615c819fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004395"
---
# <a name="spatial-data-types-sample"></a>Ejemplo de tipos de datos espaciales

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] esta aplicación de ejemplo se muestra cómo crear, insertar y recuperar tipos de datos espaciales (Geometry y Geography).
  
El archivo de código de este ejemplo se denomina SpatialDataTypes.java y se encuentra en la siguiente ubicación:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes  
```

## <a name="requirements"></a>Requisitos  

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Para obtener más información sobre cómo establecer la ruta de clases, vea [usar el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca del archivo JAR que se debe seleccionar, consulte [Requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo

En el ejemplo siguiente, el código de ejemplo crea una tabla denominada SpatialDataTypesTable_JDBC_Sample que contiene las columnas ' Geometry ' y ' Geography '.

En primer lugar, el ejemplo crea objetos ' Geometry ' y ' Geography ' a partir de un Well-Known Text (WKT) que representa un punto. Usa un SQLServerPreparedStatement con una consulta con parámetros para asignar los datos a cada columna en consecuencia.

Por último, en el ejemplo se insertan los datos en la tabla y se recuperan. Los datos se muestran en forma de WKT.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import com.microsoft.sqlserver.jdbc.Geography;
import com.microsoft.sqlserver.jdbc.Geometry;
import com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement;
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class SpatialDataTypes {

    private static String tableName = "SpatialDataTypesTable_JDBC_Sample";

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";
        // Establish the connection.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            dropAndCreateTable(stmt);

            // TODO: Implement Sample code
            String geoWKT = "POINT(3 40 5 6)";
            Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
            Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);

            try (SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) con
                    .prepareStatement("insert into " + tableName + " values (?, ?)");) {
                pstmt.setGeometry(1, geomWKT);
                pstmt.setGeography(2, geogWKT);
                pstmt.execute();

                SQLServerResultSet rs = (SQLServerResultSet) stmt.executeQuery("select * from " + tableName);
                rs.next();

                System.out.println("Geometry data: " + rs.getGeometry(1));
                System.out.println("Geography data: " + rs.getGeography(2));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void dropAndCreateTable(Statement stmt) throws SQLException {
        stmt.executeUpdate("if object_id('" + tableName + "','U') is not null" + " drop table " + tableName);

        stmt.executeUpdate("Create table " + tableName + " (c1 geometry, c2 geography)");
    }
}
```

## <a name="see-also"></a>Consulte también  

[Trabajar con tipos de datos JDBC](../../connect/jdbc/working-with-data-types-jdbc.md)  
  
