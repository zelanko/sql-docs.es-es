---
title: Las columnas dispersas | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2aa31ce2f41c8308025fd2648f18caf7ad8e04c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sparse-columns"></a>Columnas dispersas
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Las columnas dispersas son columnas normales que disponen de un almacenamiento optimizado para los valores NULL. Este tipo de columnas reducen los requisitos de espacio de los valores NULL a costa de una mayor sobrecarga a la hora de recuperar valores no NULL. Considere la posibilidad de utilizar columnas dispersas si el ahorro de espacio se sitúa entre el 20 y el 40 por ciento.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] controlador JDBC 3.0 admite columnas dispersas al conectarse a un [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] (o posterior) server. Puede usar [SQLServerDatabaseMetaData.getColumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md), [SQLServerDatabaseMetaData.getFunctionColumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md), o [SQLServerDatabaseMetaData.getProcedureColumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md) para determinar qué columnas son dispersas y cuál es la columna conjunto de columnas.  
  
 Los conjuntos de columnas son columnas calculadas que devuelven todas las columnas dispersas en forma de XML sin tipo. Considere la posibilidad de usar los conjuntos de columnas cuando una tabla contenga un gran número de columnas o que sea superior a 1024 o bien, cuando sea complicado realizar cualquier operación con columnas dispersas independientes. Un conjunto de columnas puede contener hasta 30.000 columnas.  
  
## <a name="example"></a>Ejemplo  
  
### <a name="description"></a>Description  
 Este ejemplo muestra cómo detectar conjuntos de columnas. También muestra cómo analizar los resultados XML del conjunto de columnas para obtener los datos de las columnas dispersas.  
  
 El primer listado de códigos es el código Transact-SQL que debería ejecutar en el servidor.  
  
 El segundo listado de códigos es el código fuente de Java. Antes de compilar la aplicación, cambie el nombre del servidor en la cadena de conexión.  
  
### <a name="code"></a>código  
  
```  
use AdventureWorks  
CREATE TABLE ColdCalling  
(  
ID int IDENTITY(1,1) PRIMARY KEY,  
[Date] date,  
[Time] time,  
PositiveFirstName nvarchar(50) SPARSE,  
PositiveLastName nvarchar(50) SPARSE,  
SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
);  
GO  
  
INSERT ColdCalling ([Date], [Time])  
VALUES ('10-13-09','07:05:24')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:00:24', 'AA', 'B')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:15:00', 'CC', 'DD')  
GO  
```  
  
### <a name="code"></a>código  
  
```  
import java.sql.*;  
  
import javax.xml.parsers.DocumentBuilder;  
import javax.xml.parsers.DocumentBuilderFactory;  
  
import org.xml.sax.InputSource;  
  
import java.io.StringReader;  
  
import org.w3c.dom.Document;  
import org.w3c.dom.Node;  
import org.w3c.dom.NodeList;  
  
public class SparseColumns {  
  
   public static void main(String args[]) {  
      final String connectionUrl = "jdbc:sqlserver://my_server;databaseName=AdventureWorks;integratedSecurity=true;";  
  
      Connection conn = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         conn = DriverManager.getConnection(connectionUrl);  
  
         stmt = conn.createStatement();  
         // Determine the column set column  
         String columnSetColName = null;  
         String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";  
         rs = stmt.executeQuery(strCmd);  
  
         if (rs.next()) {  
            columnSetColName = rs.getString(1);  
            System.out.println(columnSetColName + " is the column set column!");  
         }  
         rs.close();  
  
         rs = null;   
  
         strCmd = "SELECT * FROM ColdCalling";  
         rs = stmt.executeQuery(strCmd);  
  
         // Iterate through the result set  
         ResultSetMetaData rsmd = rs.getMetaData();  
  
         DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();  
         DocumentBuilder db = dbf.newDocumentBuilder();  
         InputSource is = new InputSource();  
         while (rs.next()) {  
            // Iterate through the columns  
            for (int i = 1; i <= rsmd.getColumnCount(); ++i) {  
               String name = rsmd.getColumnName(i);  
               String value = rs.getString(i);  
  
               // If this is the column set column  
               if (name.equalsIgnoreCase(columnSetColName)) {  
                  System.out.println(name);  
  
                  // Instead of printing the raw XML, parse it  
                  if (value != null) {  
                     // Add artificial root node "sparse" to ensure XML is well formed  
                     String xml = "<sparse>" + value + "</sparse>";  
  
                     is.setCharacterStream(new StringReader(xml));  
                     Document doc = db.parse(is);  
  
                     // Extract the NodeList from the artificial root node that was added  
                     NodeList list = doc.getChildNodes();  
                     // This is the <sparse> node  
                     Node root = list.item(0);   
                     // These are the xml column nodes  
                     NodeList sparseColumnList = root.getChildNodes();   
  
                     // Iterate through the XML document  
                     for (int n = 0; n < sparseColumnList.getLength(); ++n) {  
                        Node sparseColumnNode = sparseColumnList.item(n);  
                        String columnName = sparseColumnNode.getNodeName();  
                        // Note that the column value is not in the sparseColumNode, it is the value of the first child of it  
                        Node sparseColumnValueNode = sparseColumnNode.getFirstChild();  
                        String columnValue = sparseColumnValueNode.getNodeValue();  
  
                        System.out.println("\t" + columnName + "\t: " + columnValue);  
                     }  
                  }  
               } else {   // Just print the name + value of non-sparse columns  
                  System.out.println(name + "\t: " + value);  
               }  
            }  
            System.out.println();//New line between rows  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      } finally {  
         if (rs != null) {  
            try {  
               rs.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (stmt != null) {  
            try {  
               stmt.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (conn != null) {  
            try {  
               conn.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
      }  
   }        
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
