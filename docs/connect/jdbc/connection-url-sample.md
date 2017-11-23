---
title: "Ejemplo de dirección URL de conexión | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: "28"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d56838ebc82da11040c2ace7ce7accfebb0144e3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="connection-url-sample"></a>Ejemplo de URL de conexión
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esto [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante una dirección URL de conexión. También se muestra cómo recuperar los datos de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante una instrucción SQL.  
  
 El archivo de código para este ejemplo se llama connectURL.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación de*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\connections  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe establecer la ruta de clase para incluir el archivo sqljdbc.jar o sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". También necesitará acceso a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. Para obtener más información sobre cómo establecer la ruta de clase, consulte [con el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona sqljdbc.jar y sqljdbc4.jar los archivos de biblioteca de clases que se usan según su configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el código de ejemplo establece varias propiedades de conexión en la dirección URL de conexión y, a continuación, llama al método getConnection de la clase DriverManager para devolver un [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
 A continuación, el código de ejemplo utiliza la [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) método del objeto SQLServerConnection para crear un [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto y, a continuación, el [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) (método) se llama para ejecutar la instrucción SQL.  
  
 Por último, el ejemplo usa el [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto devuelto desde el método executeQuery para recorrer en iteración los resultados devueltos por la instrucción SQL.  
  
```java  
import java.sql.*;  
  
public class connectURL {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
         "databaseName=AdventureWorks;user=UserName;password=*****";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns some data.  
         String SQL = "SELECT TOP 10 * FROM Person.Contact";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println(rs.getString(4) + " " + rs.getString(6));  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Conexión y recuperación de datos](../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
