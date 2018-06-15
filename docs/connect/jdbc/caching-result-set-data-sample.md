---
title: Ejemplos de datos de conjunto de almacenamiento en caché de resultados | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ef120e92505134ef98b772a5ab2a5b3f51402ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832407"
---
# <a name="caching-result-set-data-sample"></a>Almacenar en caché ejemplos de datos de conjunto de resultados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esto [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] aplicación de ejemplo muestra cómo recuperar un conjunto grande de datos de una base de datos y, a continuación, controlar el número de filas de datos que se almacenan en caché en el cliente mediante el uso de la [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método de la [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
> [!NOTE]  
>  La limitación del número de filas almacenadas en la memoria caché del cliente es distinta de la limitación del número total de filas que contiene el conjunto de resultados. Para controlar el número total de filas que se encuentran en un conjunto de resultados, utilice la [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto, que es heredado por ambos el [ SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) objetos.  
  
 Para establecer un límite en el número de filas que se almacenan en caché en el cliente, debe usar un cursor de servidor cuando se crea uno de los objetos Statement específicamente que indica el tipo de cursor que se usará al crear el objeto de instrucción. Por ejemplo, el controlador JDBC proporciona el tipo de cursor TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, que es un solo avance rápido, cursor de servidor de solo lectura para su uso con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos.  
  
> [!NOTE]  
>  Una alternativa al tipo de cursor específico de SQL Server es usar la propiedad de cadena de conexión selectMethod y establecer su valor en "cursor". Para obtener más información acerca de los tipos de cursor compatibles con el controlador JDBC, consulte [descripción de tipos de Cursor](../../connect/jdbc/understanding-cursor-types.md).  
  
 Después de que ha ejecutado la consulta contenida en el objeto de instrucción y los datos se devuelven al cliente como un conjunto de resultados, puede llamar al método setFetchSize para controlar la cantidad de datos se recupera de la base de datos al mismo tiempo. Por ejemplo, si tiene una tabla que contiene 100 filas de datos y establece el tamaño de captura en 10, solo se almacenan en la memoria caché del cliente 10 filas de datos en un momento dado. Aunque esto reduce la velocidad del procesamiento de datos, ofrece la ventaja de usar menos memoria en el cliente, lo que puede resultar especialmente útil si necesita procesar grandes cantidades de datos.  
  
 El archivo de código para este ejemplo se llama cacheRS.java y se encuentra en la siguiente ubicación:  
  
 \<*directorio de instalación de*> \sqljdbc_\<*versión*>\\<*lenguaje*> \samples\resultsets  
  
## <a name="requirements"></a>Requisitos  
 Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo sqljdbc.jar o el archivo sqljdbc4.jar. Si en la ruta de clase falta una entrada para sqljdbc.jar o sqljdbc4.jar, la aplicación de ejemplo produce la excepción común "Clase no encontrada". También necesitará acceso a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. Para obtener más información sobre cómo establecer la ruta de clase, consulte [con el controlador JDBC](../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona sqljdbc.jar y sqljdbc4.jar los archivos de biblioteca de clases que se usan según su configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el código de ejemplo realiza una conexión a la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] base de datos de ejemplo. A continuación, usa una instrucción SQL con el [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto, especifica el tipo de cursor de servidor y, a continuación, se ejecuta la instrucción SQL y coloca los datos que devuelve en un objeto SQLServerResultSet.  
  
 A continuación, el código de ejemplo llama al método de timerTest personalizado, pasar como argumentos el tamaño de captura que se usará y el conjunto de resultados. El método timerTest, a continuación, Establece el tamaño de captura del conjunto mediante el método setFetchSize de resultados, Establece la hora de inicio de la prueba y, a continuación, recorre en iteración el conjunto de resultados con un `While` bucle. Tan pronto como el `While` se sale de dicho bucle, el código establece la hora de detención de la prueba y, a continuación, muestra el resultado de la prueba, incluidos el tamaño de captura, el número de filas procesadas, y el tiempo tardó en ejecutarse la prueba.  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
  
public class cacheRS {  
  
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
  
         // Create and execute an SQL statement that returns a large  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Sales.SalesOrderDetail;";  
         stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, +  
               SQLServerResultSet.CONCUR_READ_ONLY);  
  
         // Perform a fetch for every row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1, rs);  
         rs.close();  
  
         // Perform a fetch for every tenth row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(10, rs);  
         rs.close();  
  
         // Perform a fetch for every 100th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(100, rs);  
         rs.close();  
  
         // Perform a fetch for every 1000th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1000, rs);  
         rs.close();  
  
         // Perform a fetch for every 128th row (the default) in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(0, rs);  
         rs.close();  
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
  
   private static void timerTest(int fetchSize, ResultSet rs) {  
      try {  
  
         // Declare the variables for tracking the row count and elapsed time.  
         int rowCount = 0;  
         long startTime = 0;  
         long stopTime = 0;  
         long runTime = 0;  
  
         // Set the fetch size then iterate through the result set to  
         // cache the data locally.  
         rs.setFetchSize(fetchSize);  
         startTime = System.currentTimeMillis();  
         while (rs.next()) {  
            rowCount++;  
         }  
         stopTime = System.currentTimeMillis();  
         runTime = stopTime - startTime;  
  
         // Display the results of the timer test.  
         System.out.println("FETCH SIZE: " + rs.getFetchSize());  
         System.out.println("ROWS PROCESSED: " + rowCount);  
         System.out.println("TIME TO EXECUTE: " + runTime);  
         System.out.println();  
  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Trabajo con conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)  
  
  
