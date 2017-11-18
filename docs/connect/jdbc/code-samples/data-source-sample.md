---
title: Ejemplo de origen de datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9cda7cac56de964c97b2f60d416cbb83ff4e2b80
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-sample"></a>Ejemplo de origen de datos
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esto [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo conectarse a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos mediante un objeto de origen de datos. También se muestra cómo recuperar los datos de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos mediante un procedimiento almacenado.  
  
 El archivo de código para este ejemplo se llama connectDS.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación de*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\connections  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe establecer la ruta de clase para incluir el archivo sqljdbc.jar o sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". También necesitará acceso a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. Para obtener más información sobre cómo establecer la ruta de clase, consulte [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona sqljdbc.jar y sqljdbc4.jar los archivos de biblioteca de clases que se usan según su configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el código de ejemplo establece varias propiedades de conexión mediante el uso de métodos de establecimiento de la [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto y, a continuación, llama el [getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) método de la Objeto SQLServerDataSource para devolver un [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
 A continuación, el código de ejemplo utiliza la [prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método del objeto SQLServerConnection para crear un [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto y, a continuación, el [executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) método se llama para ejecutar el procedimiento almacenado.  
  
 Por último, el ejemplo usa el [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto devuelto desde el método executeQuery para recorrer en iteración los resultados devueltos por el procedimiento almacenado.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class connectDS {  
  
   public static void main(String[] args) {  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      CallableStatement cstmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.   
         SQLServerDataSource ds = new SQLServerDataSource();  
         ds.setUser("UserName");  
         ds.setPassword("*****");  
         ds.setServerName("localhost");  
         ds.setPortNumber(1433);   
         ds.setDatabaseName("AdventureWorks");  
         con = ds.getConnection();  
  
         // Execute a stored procedure that returns some data.  
         cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");  
         cstmt.setInt(1, 50);  
         rs = cstmt.executeQuery();  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println("EMPLOYEE: " + rs.getString("LastName") +   
               ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER: " + rs.getString("ManagerLastName") +   
               ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (cstmt != null) try { cstmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
         System.exit(1);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Conectarse y recuperar datos](../../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  

