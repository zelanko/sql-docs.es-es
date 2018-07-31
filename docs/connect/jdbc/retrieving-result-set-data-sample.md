---
title: Recuperar conjunto de resultados muestra de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1b190c36-3d38-49a2-8599-612329675851
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4d073fb21077bc5873dcb55be452e32ee5a0af3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38039199"
---
# <a name="retrieving-result-set-data-sample"></a>Recuperar ejemplos de datos de conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] muestra cómo recuperar un conjunto de datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y luego cómo mostrar esos datos.  
  
 El archivo de código para este ejemplo se llama retrieveRS.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo sqljdbc.jar o el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases sqljdbc.jar y sqljdbc4.jar que hay que usar en función de la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, el código de ejemplo realiza una conexión a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Luego, mediante una instrucción SQL con el objeto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), ejecuta la instrucción SQL y coloca los datos devueltos en un objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 Después, el código de ejemplo llama al método displayRow personalizado para recorrer en iteración las filas de datos que contiene el conjunto de resultados y usa el método [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) para mostrar algunos de los datos incluidos.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Trabajo con conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)  
  
  
