---
title: Ejemplo de dirección URL de conexión | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6d42e7743e7fba02992e641c18609371b2d1e5a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028348"
---
# <a name="connection-url-sample"></a>Ejemplo de dirección URL de conexión

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo conectar con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante una dirección URL de conexión. Además, se indica cómo recuperar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con una instrucción SQL.

El archivo de código para este ejemplo se denomina ConnectURL.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de acceso de clase, consulte [Usar el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información sobre el archivo JAR que se debe seleccionar, vea [Requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código establece varias propiedades de conexión en la dirección URL de conexión y, después, llama al método getConnection de la clase DriverManager para devolver un objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).

Después, el código usa el método [createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) del objeto SQLServerConnection para crear un objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) y, luego, se llama al método [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) para ejecutar la instrucción SQL.

Finalmente, el ejemplo usa el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) devuelto por el método executeQuery para iterar por los resultados devueltos por la instrucción SQL.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectURL {
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT TOP 10 * FROM Person.Contact";
            ResultSet rs = stmt.executeQuery(SQL);

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println(rs.getString("FirstName") + " " + rs.getString("LastName"));
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>Consulte también

[Conexión y recuperación de datos](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)
