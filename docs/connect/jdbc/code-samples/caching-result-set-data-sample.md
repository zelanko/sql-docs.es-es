---
title: Ejemplos de datos de conjunto de almacenamiento en caché de resultados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ed4174dcd164163307259100e752d277f9b200c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47823983"
---
# <a name="caching-result-set-data-sample"></a>Almacenar en caché ejemplos de datos de conjunto de resultados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

En esta aplicación de ejemplo de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se muestra cómo recuperar un conjunto de datos grande de una base de datos y, después, cómo controlar el número de filas de datos almacenadas en la memoria caché del cliente con el método [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
> [!NOTE]  
> La limitación del número de filas almacenadas en la memoria caché del cliente es distinta de la limitación del número total de filas que contiene el conjunto de resultados. Para controlar el número total de filas que contiene un conjunto de resultados, use el método [setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) del objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), que heredan los objetos [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md).  
  
Para establecer el límite del número de filas almacenadas en la memoria caché del cliente, primero debe usar un cursor de servidor para crear uno de los objetos Statement, para lo que debe especificar el tipo de cursor que se va a usar al crear el objeto Statement. Por ejemplo, JDBC Driver proporciona el tipo de cursor TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, que es un cursor de servidor de solo avance rápido y solo lectura para su uso con las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Una alternativa al tipo de cursor específico de SQL Server es usar la propiedad de cadena de conexión selectMethod y establecer su valor en "cursor". Para obtener más información acerca de los tipos de cursor compatibles con el controlador JDBC, consulte [descripción de tipos de Cursor](../../../connect/jdbc/understanding-cursor-types.md).  
  
Una vez ejecutada la consulta en el objeto Statement y devueltos los datos al cliente como un conjunto de resultados, puede llamar al método setFetchSize para controlar la cantidad de datos recuperados desde la base de datos cada vez. Por ejemplo, si tiene una tabla que contiene 100 filas de datos y establece el tamaño de captura en 10, solo se almacenan en la memoria caché del cliente 10 filas de datos en todo momento. Aunque esto reduce la velocidad del procesamiento de datos, ofrece la ventaja de usar menos memoria en el cliente, lo que puede resultar especialmente útil si necesita procesar grandes cantidades de datos.  
  
El archivo de código de este ejemplo se denomina CacheResultSet.java y se encuentra en la siguiente ubicación:  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets  
```

## <a name="requirements"></a>Requisitos  

Para ejecutar esta aplicación de ejemplo, debe configurar la ruta de clase para que incluya el archivo mssql-jdbc.jar. Además, debe tener acceso a la base de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Para obtener más información sobre cómo establecer la ruta de clase, vea [con el controlador JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] proporciona los archivos de biblioteca de clases mssql-jdbc que se usan según la configuración preferida de Java Runtime Environment (JRE). Para obtener más información acerca de qué archivo JAR para elegir, consulte [requisitos del sistema para el controlador JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  

## <a name="example"></a>Ejemplo  

En el siguiente ejemplo, el código de ejemplo realiza una conexión a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Después, usa una instrucción SQL con el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), especifica el tipo de cursor de servidor y, luego, ejecuta la instrucción SQL y coloca los datos que devuelve en un objeto SQLServerResultSet.  
  
Después, el código llama al método timerTest personalizado y pasa como argumentos el tamaño de captura que se va a usar y el conjunto de resultados. El método timerTest establece el tamaño de recuperación del conjunto de resultados con el método setFetchSize, establece la hora de inicio de la prueba y, luego, itera por el conjunto de resultados con un bucle `While`. En cuanto sale del bucle `While`, el código establece la hora de detención de la prueba y, después, muestra el resultado de dicha prueba, incluidos el tamaño de recuperación, el número de filas procesadas y el tiempo que se ha tardado en ejecutar la prueba.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class CacheResultSet {

    @SuppressWarnings("serial")
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, SQLServerResultSet.CONCUR_READ_ONLY);) {

            String SQL = "SELECT * FROM Sales.SalesOrderDetail;";

            for (int n : new ArrayList<Integer>() {
                {
                    add(1);
                    add(10);
                    add(100);
                    add(1000);
                    add(0);
                }
            }) {
                // Perform a fetch for every nth row in the result set.
                try (ResultSet rs = stmt.executeQuery(SQL)) {
                    timerTest(n, rs);
                }
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void timerTest(int fetchSize,
            ResultSet rs) throws SQLException {

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
    }
}
```

## <a name="see-also"></a>Ver también  

[Trabajo con conjuntos de resultados](../../../connect/jdbc/code-samples/working-with-result-sets.md)  
