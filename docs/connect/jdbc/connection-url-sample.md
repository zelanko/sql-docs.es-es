---
title: Ejemplo de dirección URL de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00a82318e9fc77b21e9e634e612d5d65a7ed5137
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278667"
---
# <a name="connection-url-sample"></a>Ejemplo de URL de conexión
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] se muestra cómo conectar con una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante una dirección URL de conexión. Además, se indica cómo recuperar los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con una instrucción SQL.  
  
 El archivo de código para este ejemplo se denomina ConnectURL.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\connections  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, el código establece varias propiedades de conexión en la dirección URL de conexión y, después, llama al método getConnection de la clase DriverManager para devolver un objeto [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
 Después, el código usa el método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) del objeto SQLServerConnection para crear un objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) y, luego, se llama al método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) para ejecutar la instrucción SQL.  
  
 Finalmente, el ejemplo usa el objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) devuelto por el método executeQuery para iterar por los resultados devueltos por la instrucción SQL.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Conexión y recuperación de datos](../../connect/jdbc/connecting-and-retrieving-data.md)
