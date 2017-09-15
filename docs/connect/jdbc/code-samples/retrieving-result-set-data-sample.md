---
title: Recuperar conjunto de resultados muestra de datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cd100d639e80ff9b6c78d17593cc30abfa7b7911
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-result-set-data-sample"></a>Recuperar ejemplos de datos de conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esto [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo recuperar un conjunto de datos de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] la base de datos y, a continuación, mostrar dichos datos.  
  
 El archivo de código para este ejemplo se llama retrieveRS.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación de*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo sqljdbc.jar o el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". También necesitará acceso a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. Para obtener más información sobre cómo establecer la ruta de clase, consulte [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona sqljdbc.jar y sqljdbc4.jar los archivos de biblioteca de clases que se usan según su configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el código de ejemplo realiza una conexión a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. A continuación, usar una instrucción SQL con el [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) de objeto, se ejecuta la instrucción SQL y coloca los datos que devuelve en una [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
 A continuación, el código de ejemplo llama al método displayRow personalizado para recorrer en iteración las filas de datos que se encuentran en el conjunto de resultados y utiliza el [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) método para mostrar algunos de los datos que contiene.  
  
```java
import java.sql.*;  
  
public class retrieveRS {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
            "databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns a  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Production.Product;";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
         displayRow("PRODUCTS", rs);  
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
 [Trabajar con conjuntos de resultados](../../../connect/jdbc/working-with-result-sets.md)  
  
  
