---
title: Modificar el resultado conjunto de muestra de datos | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e46eec18eca6123839034fec1fb5b3e5aadbcd0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624043"
---
# <a name="modifying-result-set-data-sample"></a>Modificar ejemplos de datos de conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo recuperar un conjunto de datos actualizable de una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Después, mediante los métodos del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md), inserta, modifica y, finalmente, elimina un fila de datos del conjunto de datos.

El archivo de código para este ejemplo se denomina UpdateResultSet.java y se encuentra en la siguiente ubicación:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>Requisitos

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Ejemplo

En el siguiente ejemplo, el código de ejemplo realiza una conexión a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Luego, mediante una instrucción SQL con el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), ejecuta la instrucción SQL y coloca los datos devueltos en un objeto SQLServerResultSet actualizable.

Después, el código de ejemplo usa el método [moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) para mover el cursor del conjunto de resultados a la fila de inserción, usa una serie de métodos [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) para insertar los datos en la nueva fila y, luego, llama al método [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) para volver a almacenar la nueva fila de datos en la base de datos.

Una vez insertada la nueva fila de datos, el código usa una instrucción SQL para recuperar la fila insertada previamente y, luego, usa la combinación de los métodos updateString y [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para actualizar la fila de datos y volver a almacenarla en la base de datos.

Por último, el código recupera la fila de datos actualizada previamente y, después, la elimina de la base de datos con el método [deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md).

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateResultSet {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);) {

            // Create and execute an SQL statement, retrieving an updateable result set.
            String SQL = "SELECT * FROM HumanResources.Department;";
            ResultSet rs = stmt.executeQuery(SQL);

            // Insert a row of data.
            rs.moveToInsertRow();
            rs.updateString("Name", "Accounting");
            rs.updateString("GroupName", "Executive General and Administration");
            rs.updateString("ModifiedDate", "08/01/2006");
            rs.insertRow();

            // Retrieve the inserted row of data and display it.
            SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";
            rs = stmt.executeQuery(SQL);
            displayRow("ADDED ROW", rs);

            // Update the row of data.
            rs.first();
            rs.updateString("GroupName", "Finance");
            rs.updateRow();

            // Retrieve the updated row of data and display it.
            rs = stmt.executeQuery(SQL);
            displayRow("UPDATED ROW", rs);

            // Delete the row of data.
            rs.first();
            rs.deleteRow();
            System.out.println("ROW DELETED");
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
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));
            System.out.println();
        }
    }
}

```

## <a name="see-also"></a>Ver también

[Trabajo con conjuntos de resultados](../../../connect/jdbc/code-samples/working-with-result-sets.md)
