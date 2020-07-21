---
title: Ejemplo de tipos de datos espaciales para el controlador JDBC de MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07f05ee878f1f818e7bf500d053ef5a306477d27
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80909401"
---
# <a name="spatial-data-types-sample"></a>Ejemplo de tipos de datos espaciales

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se muestra cómo crear, insertar y recuperar tipos de datos espaciales (Geometry y Geography).
  
El archivo de código de este ejemplo se denomina SpatialDataTypes.java y se encuentra en la siguiente ubicación:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes  
```

## <a name="requirements"></a>Requisitos  

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Para obtener más información sobre cómo establecer la ruta de acceso de clase, consulte [Usar el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca del archivo JAR que se debe seleccionar, consulte [Requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código de ejemplo crea una tabla llamada SpatialDataTypesTable_JDBC_Sample que contiene las columnas 'Geometry' y 'Geography'.

En el ejemplo, en primer lugar, se crean los objetos 'Geometry' y 'Geography' a partir de una instancia de Well-Known-Text (WKT) que representa una clase POINT. Usa una instrucción SQLServerPreparedStatement con una consulta con parámetros para asignar los datos a cada columna en consecuencia.

Por último, en el ejemplo se insertan los datos en la tabla y se recuperan. Los datos se muestran con el formato WKT.

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

[Trabajo con tipos de datos JDBC](../../connect/jdbc/working-with-data-types-jdbc.md)  
  
