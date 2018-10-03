---
title: Ejemplo de tipos de datos espaciales | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce1fc22b5cc953d79e3faacb609d2a2e10ed14fc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742865"
---
# <a name="spatial-data-types-sample"></a>Ejemplo de tipos de datos espaciales

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Esto [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo crear, insertar y recuperar tipos de datos espaciales (geometría y geografía).
  
El archivo de código de este ejemplo se denomina SpatialDataTypes.java y se encuentra en la siguiente ubicación:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes  
```

## <a name="requirements"></a>Requisitos  

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo

En el ejemplo siguiente, el código de ejemplo crea una tabla denominada SpatialDataTypesTable_JDBC_Sample que contiene las columnas 'Geometría' y 'Geography'.

El ejemplo crea primero objetos 'Geometría' y 'Geography' desde un Well-Known-Text (WKT) que representa un punto. SQLServerPreparedStatement usa con una consulta parametrizada para asignar los datos para cada columna en consecuencia.

Por último, el ejemplo inserta los datos en la tabla y lo recupera. Los datos se muestran en forma de WKT.

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

## <a name="see-also"></a>Ver también  

[Trabajar con tipos de datos &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)  
  
