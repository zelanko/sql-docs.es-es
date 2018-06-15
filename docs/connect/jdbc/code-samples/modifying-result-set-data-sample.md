---
title: Modificar conjunto de resultados muestra de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b2f8566607ec119aaa61a29468c7fca6388b5e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32831950"
---
# <a name="modifying-result-set-data-sample"></a>Modificar ejemplos de datos de conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esto [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo recuperar un conjunto de datos de actualizable una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] base de datos. A continuación, usar métodos de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) de objeto, que inserta, modifica y, finalmente, elimina una fila de datos del conjunto de datos.  
  
 El archivo de código para este ejemplo se llama updateRS.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación de*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo sqljdbc.jar o el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". También necesitará acceso a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. Para obtener más información sobre cómo establecer la ruta de clase, consulte [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona sqljdbc.jar y sqljdbc4.jar los archivos de biblioteca de clases que se usan según su configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el código de ejemplo realiza una conexión a la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. A continuación, usar una instrucción SQL con el [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) de objeto, se ejecuta la instrucción SQL y coloca los datos que devuelve en un objeto SQLServerResultSet actualizable.  
  
 A continuación, el código de ejemplo utiliza la [moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) método para mover el conjunto de resultados cursor a la fila de inserción, se usa una serie de [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) métodos para insertar datos en la nueva fila y, a continuación, llama a la [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) método para almacenar la nueva fila de datos a la base de datos.  
  
 Después de insertar la nueva fila de datos, el código de ejemplo utiliza una instrucción SQL para recuperar la fila insertada previamente y, a continuación, usa la combinación de updateString y [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) métodos para actualizar la fila de datos y vuelva a enviarlo de nuevo a la base de datos.  
  
 Por último, el código de ejemplo recupera la fila de datos actualizada previamente y, a continuación, se elimina de la base de datos mediante la [deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) método.  
  
```java
import java.sql.*;  
  
public class updateRS {  
  
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
  
         // Create and execute an SQL statement, retrieving an updateable result set.  
         String SQL = "SELECT * FROM HumanResources.Department;";  
         stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);  
  
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
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));  
            System.out.println();  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Trabajo con conjuntos de resultados](../../../connect/jdbc/working-with-result-sets.md)  
  
  
