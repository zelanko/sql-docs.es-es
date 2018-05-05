---
title: Uso de copia masiva con el controlador JDBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6daf0ae2773d8a99e4f9264c05024a86fcd79926
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>Uso de la copia masiva con el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft SQL Server incluye una conocida utilidad de línea de comandos denominada **bcp** para rápidamente copie de forma masiva archivos grandes en tablas o vistas de bases de datos de SQL Server. La clase SQLServerBulkCopy permite escribir soluciones de código en Java que proporcionan una funcionalidad similar. Hay otras maneras de cargar datos en una tabla de SQL Server (las instrucciones INSERT, por ejemplo) pero SQLServerBulkCopy ofrece una importante ventaja de rendimiento sobre ellas.  
  
 La clase SQLServerBulkCopy puede usarse para escribir datos solo en tablas de SQL Server. Pero el origen de los datos no se limita a SQL Server; puede utilizarse cualquier origen de datos, siempre y cuando los datos se puedan leer con una implementación ResultSet, RowSet o ISQLServerBulkRecord.  
  
 Al usar la clase SQLServerBulkCopy puede llevar a cabo:  
  
-   Una única operación de copia masiva.  
  
-   Varias operaciones de copia masiva.  
  
-   Una operación de copia masiva con una transacción  
  
> [!NOTE]  
>  Cuando se usa el Microsoft JDBC Driver 4.1 para SQL Server o versiones anteriores (que no admite la clase SQLServerBulkCopy), puede ejecutar la instrucción BULK INSERT de SQL Server Transact-SQL en su lugar.  
  
## <a name="bulk-copy-example-setup"></a>Configuración de ejemplo de copia masiva  
 La clase SQLServerBulkCopy puede usarse para escribir datos solo en tablas de SQL Server. Los ejemplos de código que se muestran en este tema usan AdventureWorks, la base de datos de muestra de SQL Server. Para evitar modificar los ejemplos de código de las tablas existentes escriba los datos en tablas que tendrá que crear en primer lugar.  
  
 Las tablas BulkCopyDemoMatchingColumns y BulkCopyDemoDifferentColumns se basan en la tabla AdventureWorks Production.Products. En los ejemplos de código que usan estas tablas, los datos se agregan desde la tabla Production.Products a una de estas tablas de muestra. La tabla BulkCopyDemoDifferentColumns se usa cuando el ejemplo muestra cómo asignar columnas de los datos de origen a la tabla de destino; BulkCopyDemoMatchingColumns se usa para la mayoría de los otros ejemplos.  
  
 Algunos de los ejemplos de código muestran cómo usar una clase SQLServerBulkCopy para escribir en varias tablas. En estos ejemplos, se usan las tablas BulkCopyDemoOrderHeader y BulkCopyDemoOrderDetail como las tablas de destino. Estas tablas se basan en las tablas Sales.SalesOrderHeader y Sales.SalesOrderDetail en Adventure Works.  
  
> [!NOTE]  
>  Los ejemplos de código SQLServerBulkCopy se proporcionan para mostrar la sintaxis para usar solo SQLServerBulkCopy. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción Transact-SQL INSERT... Instrucción SELECT para copiar los datos.  
  
###  <a name="BKMK_TableSetup"></a> Programa de instalación de la tabla  
 Para crear las tablas necesarias para que los ejemplos de código se ejecuten correctamente, debe ejecutar las siguientes instrucciones de Transact-SQL en una base de datos de SQL Server.  
  
```  
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED   
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED   
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED   
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')   
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED   
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```  
  
## <a name="single-bulk-copy-operations"></a>Operaciones de copia masiva únicas.  
 El método más sencillo para realizar una operación de copia masiva de SQL Server es realizar una operación única con una base de datos. De forma predeterminada, una operación de copia masiva se realiza como una operación aislada: la operación de copia tiene lugar sin transacciones y no es posible revertirla.  
  
> [!NOTE]  
>  Si necesita revertir toda o parte de la copia masiva cuando se produce un error, puede usar una transacción administrada por SQLServerBulkCopy o realizar la operación de copia masiva en una transacción existente.  
>   
>  Para obtener más información, vea [operaciones de copia masiva y transacción](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TransactionBulk)  
  
 Los pasos generales para realizar una operación de copia masiva son:  
  
1.  Conéctese al servidor de origen y obtenga los datos que se van a copiar. Los datos también pueden proceder de otros orígenes, si se pueden recuperar de un objeto ResultSet o una implementación ISQLServerBulkRecord.  
  
2.  Conectarse al servidor de destino (a menos que desee **SQLServerBulkCopy** para establecer una conexión automáticamente).  
  
3.  Crear un objeto SQLServerBulkCopy y configure las propiedades necesarias a través de **setBulkCopyOptions**.  
  
4.  Llame a la **setDestinationTableName** método para indicar la tabla de destino para la mayor parte de operación de inserción.  
  
5.  Llame a uno de los **writeToServer** métodos.  
  
6.  Opcionalmente, actualice las propiedades a través de **setBulkCopyOptions** y llame a **writeToServer** nuevo según sea necesario.  
  
7.  Llame a **cerrar**, o incluya las operaciones de copia masiva en una instrucción try con recursos.  
  
> [!CAUTION]  
>  Se recomienda que los tipos de datos de la columna de origen y de destino coincidan. Si los tipos de datos no coinciden, SQLServerBulkCopy intentará convertir los valores de origen al tipo de datos de destino. Las conversiones pueden afectar al rendimiento y también pueden producir errores inesperados. Por ejemplo, un tipo de datos double puede convertirse a un tipo de datos decimal la mayoría de las veces, pero no siempre.  
  
### <a name="example"></a>Ejemplo  
 La aplicación siguiente muestra cómo cargar datos mediante la clase SQLServerBulkCopy. En este ejemplo, se usa ResultSet para copiar datos de la tabla Production.Product en la base de datos de AdventureWorks de SQL Server a una tabla similar en la misma base de datos.  
  
> [!IMPORTANT]  
>  Este ejemplo no se ejecutará a menos que haya creado las tablas de trabajo como se describe en [el programa de instalación de la tabla](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Este código se proporciona para mostrar la sintaxis para usar solo SQLServerBulkCopy. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción Transact-SQL INSERT... Instrucción SELECT para copiar los datos.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
                        // Open the destination connection. In the real world you would    
                        // not use SQLServerBulkCopy to move data from one table to the other    
                        // in the same database. This is for demonstration purposes only.   
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            // Set up the bulk copy object.    
                            // Note that the column positions in the source   
                            // table match the column positions in    
                            // the destination table so there is no need to   
                            // map columns.   
                            try (SQLServerBulkCopy bulkCopy =  
                                       new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                try  
                                {  
                                    // Write from the source to the destination.  
                                    bulkCopy.writeToServer(rsSourceData);  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                }  
                            }  
  
                            // Perform a final count on the destination    
                            // table to see how many rows were added.  
                            try (ResultSet rsRowCount = stmt.executeQuery(  
                                    "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                            {  
                                rsRowCount.next();  
                                long countEnd = rsRowCount.getInt(1);  
                                System.out.println("Ending row count = " + countEnd);  
                                System.out.println((countEnd - countStart) + " rows were added.");  
                            }  
                        }  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Realizar una operación de copia masiva mediante Transact-SQL  
 En el ejemplo siguiente se muestra cómo utilizar el método executeUpdate para ejecutar la instrucción BULK INSERT.  
  
> [!NOTE]  
>  La ruta de acceso al origen de datos depende del servidor. El proceso del servidor debe tener acceso a esa ruta para que la operación de copia masiva se realice correctamente.  
  
```  
try (Connection con = DriverManager.getConnection(connectionString))  
{  
    try (Statement stmt = con.createStatement())  
    {  
        // Perform the BULK INSERT  
        stmt.executeUpdate(  
                "BULK INSERT Northwind.dbo.[Order Details] " +  
                        "FROM 'f:\\mydata\\data.tbl' " +  
                        "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");  
    }  
}  
```  
  
## <a name="multiple-bulk-copy-operations"></a>Varias operaciones de copia masiva.  
 Puede realizar varias operaciones de copia masiva con una única instancia de una clase SQLServerBulkCopy. Si los parámetros de operación cambian entre copias (por ejemplo, el nombre de la tabla de destino), debe actualizarlos antes de las subsiguientes llamadas a cualquiera de los métodos writeToServer, como se muestra en el ejemplo siguiente. A menos que se cambien explícitamente, todos los valores de propiedad permanecen igual que estaban en la operación de copia masiva anterior para una instancia determinada.  
  
> [!NOTE]  
>  Generalmente, es más eficaz realizar varias operaciones de copia masiva con la misma instancia de SQLServerBulkCopy que usar una instancia distinta para cada operación.  
  
 Si se realizan varias operaciones de copia masiva con el mismo objeto SQLServerBulkCopy, no hay restricciones en cuanto a si la información de origen o destino es igual o diferente en cada operación. Sin embargo, debe asegurarse de que la información de asociación de la columna está establecida correctamente cada vez que se escribe en el servidor.  
  
> [!IMPORTANT]  
>  Este ejemplo no se ejecutará a menos que haya creado las tablas de trabajo como se describe en [el programa de instalación de la tabla](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Este código se proporciona para mostrar la sintaxis para usar solo SQLServerBulkCopy. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción Transact-SQL INSERT... Instrucción SELECT para copiar los datos.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection1 = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection1.createStatement())  
                {  
  
                    // Empty the destination tables.   
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderHeader;");  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoOrderDetail;");  
  
                    // Perform an initial count on the destination   
                    //  table with matching columns.  
                    long countStartHeader = 0;  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        countStartHeader = rsRowCountHeader.getInt(1);  
                        System.out.println("Starting row count for Header table = " + countStartHeader);  
                    }  
  
                    // Perform an initial count on the destination   
                    // table with different column positions.  
                    long countStartDetail = 0;  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        countStartDetail = rsRowCountDetail.getInt(1);  
                        System.out.println("Starting row count for Detail table = " + countStartDetail);  
                    }  
  
                    // Get data from the source table as a ResultSet.   
                    // The Sales.SalesOrderHeader and Sales.SalesOrderDetail   
                    // tables are quite large and could easily cause a timeout   
                    // if all data from the tables is added to the destination.    
                    // To keep the example simple and quick, a parameter is     
                    // used to select only orders for a particular account    
                    // as the source for the bulk insert.  
                    try (PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(  
                            "SELECT [SalesOrderID], [OrderDate], " +  
                            "[AccountNumber] FROM [Sales].[SalesOrderHeader] " +  
                            "WHERE [AccountNumber] = ?;"))  
                    {  
                        preparedStmt1.setString(1, "10-4020-000034");  
  
                        try (ResultSet rsHeader = preparedStmt1.executeQuery())  
                        {  
                            // Get the Detail data in a separate connection.   
                            try (Connection sourceConnection2 = DriverManager.getConnection(connectionString))  
                            {  
                                try (PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(  
                                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], " +  
                                                "[SalesOrderDetailID], [OrderQty], [ProductID], " +  
                                                "[UnitPrice] FROM [Sales].[SalesOrderDetail] " +  
                                                "INNER JOIN [Sales].[SalesOrderHeader] " +  
                                                "ON [Sales].[SalesOrderDetail].[SalesOrderID] " +  
                                                "= [Sales].[SalesOrderHeader].[SalesOrderID] " +  
                                                "WHERE [AccountNumber] = ?;"))  
                                {  
                                    preparedStmt2.setString(1, "10-4020-000034");  
  
                                    try (ResultSet rsDetail = preparedStmt2.executeQuery())  
                                    {  
                                        // Create the SQLServerBulkCopySQLServerBulkCopy object.    
                                        try (SQLServerBulkCopy bulkCopy =  
                                                   new SQLServerBulkCopy(connectionString))  
                                        {  
                                            bulkCopy.setBulkCopyOptions(copyOptions);  
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderHeader");  
  
                                            // Guarantee that columns are mapped correctly by   
                                            // defining the column mappings for the order.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping("OrderDate", "OrderDate");  
                                            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");  
  
                                            // Write rsHeader to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsHeader);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
  
                                            // Set up the order details destination.   
                                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoOrderDetail");  
  
                                            // Clear the existing column mappings  
                                            bulkCopy.clearColumnMappings();  
  
                                            // Add order detail column mappings.  
                                            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");  
                                            bulkCopy.addColumnMapping(  
                                                    "SalesOrderDetailID",   
                                                    "SalesOrderDetailID");  
                                            bulkCopy.addColumnMapping("OrderQty", "OrderQty");  
                                            bulkCopy.addColumnMapping("ProductID", "ProductID");  
                                            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");  
  
                                            // Write rsDetail to the destination.   
                                            try  
                                            {  
                                                bulkCopy.writeToServer(rsDetail);  
                                            }  
                                            catch (Exception e)  
                                            {  
                                                // Handle any errors that may have occurred.  
                                                e.printStackTrace();  
                                            }  
                                        }  
                                    }  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination   
                    // tables to see how many rows were added.  
                    try (ResultSet rsRowCountHeader = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderHeader;"))  
                    {  
                        rsRowCountHeader.next();  
                        long countEndHeader =  rsRowCountHeader.getInt(1);  
                        System.out.println(  
                                (countEndHeader - countStartHeader) +   
                                " rows were added to the Header table.");  
                    }  
  
                    try (ResultSet rsRowCountDetail = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoOrderDetail;"))  
                    {  
                        rsRowCountDetail.next();  
                        long countEndDetail = rsRowCountDetail.getInt(1);  
                        System.out.println(  
                                (countEndDetail - countStartDetail) +   
                                " rows were added to the Detail table.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
##  <a name="BKMK_TransactionBulk"></a> Transacciones y operaciones de copia masiva  
 Las operaciones de copia masiva se pueden realizar como operaciones aisladas o como parte de una transacción en varios pasos. Esta última opción permite realizar más de una operación de copia masiva en la misma transacción, así como realizar otras operaciones de base de datos (como inserciones, actualizaciones y eliminaciones) mientras todavía se puede confirmar o revertir la transacción entera.  
  
 De forma predeterminada, una operación de copia masiva se realiza como una operación aislada. La operación de copia masiva tiene lugar sin transacciones y sin la oportunidad de revertirla. Si necesita revertir la totalidad o parte de la copia masiva cuando se produce un error, puede usar una transacción administrada por SQLServerBulkCopy o realizar la operación de copia masiva en una transacción existente.  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>Realizar una operación de copia masiva sin transacciones  
 La aplicación siguiente muestra lo que sucede cuando una operación de copia masiva sin transacciones encuentra un error en medio de la operación.  
  
 En el ejemplo, la tabla de origen como tabla de destino incluyen una columna de identidad denominada **ProductID**. En primer lugar, el código prepara la tabla de destino mediante la eliminación de todas las filas y, a continuación, inserta una sola fila cuyo **ProductID** se sabe que existe en la tabla de origen. De forma predeterminada, se genera un nuevo valor para la columna de identidad en la tabla de destino para cada fila agregada. En este ejemplo, cuando se abre la conexión se establece una opción que obliga al proceso de carga masiva a usar los valores de identidad de la tabla de origen en su lugar.  
  
 La operación de copia masiva se ejecuta con la **BatchSize** propiedad establecida en 10. Cuando la operación encuentra la fila no válida, se produce una excepción. En este primer ejemplo, la operación de copia masiva es sin transacciones. Se confirman todos los lotes copiados hasta el punto del error; el lote que contiene la clave duplicada se revierte y la operación de copia masiva se detiene antes de procesar el resto de los lotes.  
  
> [!NOTE]  
>  Este ejemplo no se ejecutará a menos que haya creado las tablas de trabajo como se describe en [el programa de instalación de la tabla](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Este código se proporciona para mostrar la sintaxis para usar solo SQLServerBulkCopy. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción Transact-SQL INSERT... Instrucción SELECT para copiar los datos.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.  
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection String.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
              "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>Realizar una operación de copia masiva dedicada en una transacción  
 De forma predeterminada, una operación de copia masiva es su propia transacción. Si desea realizar una operación de copia masiva dedicada, cree una nueva instancia de SQLServerBulkCopy con una cadena de conexión. En este escenario, la operación de copia masiva crea y, a continuación, confirma o revierte la transacción. Puede especificar explícitamente el **UseInternalTransaction** opción **SQLServerBulkCopyOptions** para provocar una operación de copia masiva para ejecutarla en su propia transacción, produciendo cada lote de la mayor parte de forma explícita Copie la operación se ejecute dentro de una transacción independiente.  
  
> [!NOTE]  
>  Dado que diferentes lotes se ejecutan en diferentes transacciones, si se produce un error durante la operación de copia masiva, se revertirán todas las filas del lote actual, pero las filas de los lotes anteriores permanecerán en la base de datos.  
  
 La aplicación siguiente es similar al ejemplo anterior, con una excepción: en este caso, la operación de copia masiva administra sus propias transacciones. Se confirman todos los lotes copiados hasta el punto del error; el lote que contiene la clave duplicada se revierte y la operación de copia masiva se detiene antes de procesar el resto de los lotes.  
  
> [!NOTE]  
>  Este ejemplo no se ejecutará a menos que haya creado las tablas de trabajo como se describe en [el programa de instalación de la tabla](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Este código se proporciona para mostrar la sintaxis para usar solo SQLServerBulkCopy. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción Transact-SQL INSERT... Instrucción SELECT para copiar los datos.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object.  
                        // Note that when specifying the UseInternalTransaction   
                        // option, you cannot also use an external transaction.   
                        // Therefore, you must use the SQLServerBulkCopy construct that   
                        // requires a string for the connection, rather than an   
                        // existing Connection object.   
                        SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                        copyOptions.setKeepIdentity(true);  
                        copyOptions.setBatchSize(10);  
                        copyOptions.setUseInternalTransaction(true);  
  
                        try (SQLServerBulkCopy bulkCopy =   
                                new SQLServerBulkCopy(connectionString))  
                        {  
                            bulkCopy.setBulkCopyOptions(copyOptions);  
                            bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                            // Write from the source to the destination.   
                            // This should fail with a duplicate key error   
                            // after some of the batches have been copied.   
                            try  
                            {  
                                bulkCopy.writeToServer(rsSourceData);  
                            }  
                            catch (Exception e)  
                            {  
                                // Handle any errors that may have occurred.  
                                e.printStackTrace();  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
```  
  
### <a name="using-existing-transactions"></a>Uso de transacciones existentes  
 Puede pasar un objeto de conexión que tiene las transacciones habilitadas como un parámetro en un constructor SQLServerBulkCopy. En esta situación, la operación de copia masiva se realiza en una transacción existente y el estado de la transacción no sufre ningún cambio (es decir, no se confirma ni anula). Esto permite que una aplicación incluya la operación de copia masiva en una transacción con otras operaciones de base de datos. Si se produce un error y necesita revertir toda la operación de copia masiva, o si la copia masiva debe ejecutarse como parte de un proceso más grande que se pueda revertir, puede realizar la reversión en el objeto de conexión en cualquier momento después de la operación de copia masiva.  
  
 La siguiente aplicación es similar al primer ejemplo (sin transacciones), con una diferencia: en este ejemplo, la operación de copia masiva se incluye en una transacción externa más grande. Cuando se produce la infracción de la clave principal, toda la transacción se revierte y no se agrega ninguna fila a la tabla de destino.  
  
> [!NOTE]  
>  Este ejemplo no se ejecutará a menos que haya creado las tablas de trabajo como se describe en [el programa de instalación de la tabla](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup). Este código se proporciona para mostrar la sintaxis para usar solo SQLServerBulkCopy. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción Transact-SQL INSERT... Instrucción SELECT para copiar los datos.  
  
```  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        try  
        {  
            // Note: if you are not using try-with-resources statements (as here),  
            // you must remember to call close() on any Connection, Statement,   
            // ResultSet, and SQLServerBulkCopy objects that you create.  
  
            // Open a sourceConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = sourceConnection.createStatement())  
                {  
                    //  Delete all from the destination table.  
                    stmt.executeUpdate("DELETE FROM dbo.BulkCopyDemoMatchingColumns");  
  
                    //  Add a single row that will result in duplicate key            
                    //  when all rows from source are bulk copied.            
                    //  Note that this technique will only be successful in             
                    //  illustrating the point if a row with ProductID = 446              
                    //  exists in the AdventureWorks Production.Products table.             
                    //  If you have made changes to the data in this table, change            
                    //  the SQL statement in the code to add a ProductID that            
                    //  does exist in your version of the Production.Products            
                    //  table. Choose any ProductID in the middle of the table            
                    //  (not first or last row) to best illustrate the result.  
                    stmt.executeUpdate("SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns ON;" +  
                            "INSERT INTO " + "dbo.BulkCopyDemoMatchingColumns " +  
                            "([ProductID], [Name] ,[ProductNumber]) " +  
                            "VALUES(446, 'Lock Nut 23','LN-3416');" +  
                            "SET IDENTITY_INSERT dbo.BulkCopyDemoMatchingColumns OFF");  
  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    //  Get data from the source table as a ResultSet.  
                    try (ResultSet rsSourceData = stmt.executeQuery(  
                            "SELECT ProductID, Name, ProductNumber FROM Production.Product"))  
                    {  
  
                        // Set up the bulk copy object inside the transaction.  
                        try (Connection destinationConnection =   
                                DriverManager.getConnection(connectionString))  
                        {  
                            destinationConnection.setAutoCommit(false);  
  
                            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();  
                            copyOptions.setKeepIdentity(true);  
                            copyOptions.setBatchSize(10);  
  
                            try (SQLServerBulkCopy bulkCopy =   
                                    new SQLServerBulkCopy(destinationConnection))  
                            {  
                                bulkCopy.setBulkCopyOptions(copyOptions);  
                                bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                                // Write from the source to the destination.   
                                // This should fail with a duplicate key error.   
                                try  
                                {  
                                    bulkCopy.writeToServer(rsSourceData);  
                                    destinationConnection.commit();  
                                }  
                                catch (Exception e)  
                                {  
                                    // Handle any errors that may have occurred.  
                                    e.printStackTrace();  
                                    destinationConnection.rollback();  
                                }  
                            }  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;"  
                + "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-from-a-csv-file"></a>Copia masiva desde un archivo CSV  
 La aplicación siguiente muestra cómo cargar datos mediante la clase SQLServerBulkCopy. En este ejemplo, se usa un archivo CSV para copiar datos exportados de la tabla Production.Product en la base de datos de AdventureWorks de SQL Server a una tabla similar en la base de datos.  
  
> [!IMPORTANT]  
>  Este ejemplo no se ejecutará a menos que haya creado las tablas de trabajo como se describe en [el programa de instalación de la tabla](../../ssms/download-sql-server-management-studio-ssms.md) para obtenerlo.  
  
1.  Abra **SQL Server Management Studio** y conectarse a SQL Server con la base de datos de AdventureWorks.  
  
2.  Expanda las bases de datos, haga clic con la base de datos de AdventureWorks, seleccione **tareas** y **exportar datos**...  
  
3.  Para el origen de datos, seleccione la **origen de datos** que le permite conectarse a SQL Server (por ejemplo, SQL Server Native Client 11.0), compruebe la configuración y, a continuación, **siguiente**  
  
4.  Para el destino, seleccione la **Flat File Destination** y escriba un **nombre de archivo** con un destino como C:\Test\TestBulkCSVExample.csv. Compruebe que la **formato** está delimitado, el **calificador de texto** es y habilitar **nombres de columna en la primera fila de datos**y, a continuación, seleccione **siguiente**  
  
5.  Seleccione **escribir una consulta para especificar los datos que se va a transferir** y **siguiente**.  Escriba su **instrucción SQL** seleccione ProductID, Name y ProductNumber de Production.Product y **siguiente**  
  
6.  Compruebe la configuración: puede dejar el delimitador de filas como {CR} {LF} y el delimitador de columna como coma {,}.  Seleccione **editar asignaciones**... y compruebe que los datos **tipo** es correcto para cada columna (por ejemplo, entero para ProductID y cadena Unicode para los demás).  
  
7.  Ir directamente a **finalizar** y ejecute la exportación.  
  
```  
  
import java.sql.*;  
  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;  
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;  
  
public class Program  
{  
    public static void main(String[] args)  
    {  
        String connectionString = GetConnectionString();  
        SQLServerBulkCSVFileRecord fileRecord = null;  
        try  
        {              
            // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.  
            // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.  
            fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);      
  
            // Set the metadata for each column to be copied.  
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);  
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);  
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);  
  
            // Open a destinationConnection to the AdventureWorks database.   
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
            try (Connection destinationConnection = DriverManager.getConnection(connectionString))  
            {  
                try (Statement stmt = destinationConnection.createStatement())  
                {  
                    // Perform an initial count on the destination table.  
                    long countStart = 0;  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        countStart = rsRowCount.getInt(1);  
                        System.out.println("Starting row count = " + countStart);  
                    }  
  
                    // Set up the bulk copy object.    
                    // Note that the column positions in the source   
                    // data reader match the column positions in    
                    // the destination table so there is no need to   
                    // map columns.   
                    try (SQLServerBulkCopy bulkCopy =  
                               new SQLServerBulkCopy(destinationConnection))  
                    {  
                        bulkCopy.setDestinationTableName("dbo.BulkCopyDemoMatchingColumns");  
  
                        try  
                        {  
                            // Write from the source to the destination.  
                            bulkCopy.writeToServer(fileRecord);  
                        }  
                        catch (Exception e)  
                        {  
                            // Handle any errors that may have occurred.  
                            e.printStackTrace();  
                        }  
                    }  
  
                    // Perform a final count on the destination    
                    // table to see how many rows were added.  
                    try (ResultSet rsRowCount = stmt.executeQuery(  
                            "SELECT COUNT(*) FROM dbo.BulkCopyDemoMatchingColumns;"))  
                    {  
                        rsRowCount.next();  
                        long countEnd = rsRowCount.getInt(1);  
                        System.out.println("Ending row count = " + countEnd);  
                        System.out.println((countEnd - countStart) + " rows were added.");  
                    }  
                }  
            }  
        }  
        catch (Exception e)  
        {  
            // Handle any errors that may have occurred.  
            e.printStackTrace();  
        }  
        finally  
        {  
            if (fileRecord != null) try { fileRecord.close(); } catch(Exception e) {}  
        }  
    }  
  
    // To avoid storing the sourceConnection String in your code,    
    // you can retrieve it from a configuration file.   
    private static String GetConnectionString()  
    {  
  
        // Create a variable for the connection string.  
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
           "databaseName=AdventureWorks;user=UserName;password=*****";  
  
        return connectionUrl;  
    }  
}  
  
```  
  
### <a name="bulk-copy-with-always-encrypted-columns"></a>Copia masiva con columnas siempre cifradas  
 Desde Microsoft JDBC Driver 6.0 para SQL Server, se admite la copia masiva con columnas siempre cifradas.  
  
 Dependiendo de las opciones de copia masiva y el cifrado de tipo de las tablas de origen y destino puede descifrar de forma transparente y, a continuación, cifrar los datos o el controlador JDBC puede enviar los datos cifrados tal cual. Por ejemplo, cuando se copian de forma masiva datos desde una columna cifrada a una columna sin cifrar, el controlador descifra de forma transparente datos antes de enviarlos a SQL Server. De igual forma cuando se copian de forma masiva datos desde una columna sin cifrar (o desde un archivo CSV) a una columna cifrada, el controlador cifra forma transparente los datos antes de enviarlos a SQL Server. Si tanto de origen y destino se cifra, a continuación, dependiendo de la **allowEncryptedValueModifications** opción de copia masiva del controlador enviaría datos tal y como está o descifrar los datos y cifrarlo de nuevo antes de enviarlos a SQL Server.  
  
 Para obtener más información, consulte el **allowEncryptedValueModifications** siguiente, opción de copia masiva y [usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
>  Limitación de Microsoft JDBC Driver 6.0 para SQL Server, cuando se copian datos desde un archivo CSV a columnas cifradas de forma masiva:  
>   
>  Solo el Transact-SQL predeterminada formato literal de cadena se admite para los tipos de fecha y hora  
>   
>  No se admiten tipos de datos DATETIME y SMALLDATETIME  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>API de copia masiva para el controlador JDBC  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy  
 Le permite la carga masiva de forma eficaz de una tabla de SQL Server con datos procedentes de otro origen.  
  
 Microsoft SQL Server incluye una conocida utilidad del símbolo del sistema denominada bcp para mover datos de una tabla a otra, ya sea en un único servidor o entre servidores. La clase SQLServerBulkCopy le permite escribir soluciones de código en Java que proporcionan una funcionalidad similar. Hay otras maneras de cargar datos en una tabla de SQL Server (las instrucciones INSERT, por ejemplo), pero SQLServerBulkCopy ofrece una importante ventaja de rendimiento con respecto a ellas.  
  
 La clase SQLServerBulkCopy puede usarse para escribir datos solo en tablas de SQL Server. Pero el origen de los datos no se limita a SQL Server; puede usarse cualquier origen de datos, siempre y cuando los datos se puedan leer con una instancia ResultSet o una implementación ISQLServerBulkRecord.  
  
|Constructor|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopy(Connection)|Inicializa una nueva instancia de la clase SQLServerBulkCopy usando la instancia abierta especificada de SQLServerConnection. Si la conexión tiene habilitadas las transacciones, las operaciones de copia se realizarán dentro de esa transacción.|  
|SQLServerBulkCopy (cadena connectionURL)|Inicializa y abre una nueva instancia de SQLServerConnection según el connectionurl proporcionado. El constructor usa el SQLServerConnection para inicializar una nueva instancia de la clase SQLServerBulkCopy.|  
  
|Propiedad|Description|  
|--------------|-----------------|  
|Cadena DestinationTableName|Nombre de la tabla de destino en el servidor.<br /><br /> Si no se ha establecido DestinationTableName cuando se llama a writeToServer, se produce una SQLServerException.<br /><br /> DestinationTableName es un nombre de tres partes (\<base de datos >.\< owningschema >. \<nombre >). Si quiere, puede calificar el nombre de tabla con su base de datos y esquema propietario. Sin embargo, si el nombre de tabla usa un carácter de subrayado ("_") o cualquier otro carácter especial, el nombre ha de ir entre corchetes. Para obtener más información, vea «Identificadores» en los Libros en pantalla de SQL Server.|  
|ColumnMappings|Las asignaciones de columnas definen las relaciones entre las columnas del origen de datos y las columnas en el destino.<br /><br /> Si no se definen las asignaciones, las columnas se asignan implícitamente según la posición ordinal. Para que esto funcione, los esquemas de origen y destino deben coincidir. Si no es así, se producirá una excepción.<br /><br /> Si las asignaciones no están vacías, no hay que especificar todas las columnas presentes en el origen de datos. Se ignoran aquellas que no estén asignadas.<br /><br /> Puede hacer referencia a las columnas de origen y de destino tanto por nombre como por ordinal.|  
  
|Método|Description|  
|------------|-----------------|  
|Void addColumnMapping ((sourceColumn int, int destinationColumn)|Agrega una nueva asignación de columnas, usando las posiciones ordinales para especificar tanto las columnas de origen como las de destino.|  
|Void addColumnMapping ((int sourceColumn, destinationColumn de cadena)|Agrega una nueva asignación de columnas, con un valor ordinal para la columna de origen y un nombre de columna para la columna de destino.|  
|Void addColumnMapping ((cadena sourceColumn, destinationColumn int)|Agrega una nueva asignación de columnas, con un nombre de columna para describir la columna de origen y un valor ordinal para especificar la columna de destino.|  
|Void addColumnMapping (cadena sourceColumn, destinationColumn de cadena)|Agrega una nueva asignación de columnas, usando los nombres de columna para especificar tanto las columnas de origen como las de destino.|  
|Void clearColumnMappings()|Elimina el contenido de las asignaciones de columnas.|  
|Close() void|Cierra la instancia de SQLServerBulkCopy.|  
|SQLServerBulkCopyOptions getBulkCopyOptions()|Recupera el conjunto actual de SQLServerBulkCopyOptions.|  
|Cadena getDestinationTableName()|Recupera el nombre de tabla de destino actual.|  
|Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)|Actualiza el comportamiento de la instancia SQLServerBulkCopy según las opciones proporcionadas.|  
|Void setDestinationTableName(String tableName)|Establece el nombre de la tabla de destino.|  
|Void writeToServer(ResultSet sourceData)|Copia todas las filas en el conjunto de resultados proporcionado en una tabla de destino especificada por la propiedad DestinationTableName del objeto SQLServerBulkCopy.|  
|Void writeToServer(RowSet sourceData)|Copia todas las filas del ResultSet proporcionado en una tabla de destino especificada por la propiedad DestinationTableName del objeto SQLServerBulkCopy.|  
|Void writeToServer(ISQLServerBulkRecord sourceData)|Copia todas las filas de la implementación ISQLServerBulkRecord proporcionada a una tabla de destino especificada por la propiedad DestinationTableName del objeto SQLServerBulkCopy.|  
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  
 Una colección de configuraciones que controlan cómo se comportan los métodos writeToServer en una instancia de SQLServerBulkCopy.  
  
|Constructor|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopyOptions()|Inicializa una nueva instancia de la clase SQLServerBulkCopyOptions con los valores predeterminados de todas las opciones.|  
  
 Los captadores y establecedores están disponibles para las siguientes opciones:  
  
|Opción|Description|Predeterminado|  
|------------|-----------------|-------------|  
|CheckConstraints booleano|Comprueba las restricciones mientras se insertan los datos.|False: no se comprueban las restricciones|  
|Fire_triggers booleano|Si se especifican, provoca que el servidor active los desencadenadores de inserción para las filas que se insertan en la base de datos.|False: no se activa ningún desencadenador|  
|KeepIdentity booleano|Mantiene los valores de identidad de origen.|False: el destino asigna los valores de identidad|  
|KeepNulls booleano|Conserva los valores nulos en la tabla de destino independientemente de la configuración para los valores predeterminados.|False: los valores nulos se reemplazan por valores predeterminados si procede|  
|Booleano TableLock|Obtiene un bloqueo de actualización masiva durante toda la operación de copia masiva.|False: se usan bloqueos de fila.|  
|UseInternalTransaction booleano|Si se especifica, cada lote de la operación de copia masiva tendrá lugar en una transacción. Si SQLServerBulkCopy está usando una conexión existente (como se especifica en el constructor), se producirá una SQLServerException.  Si SQLServerBulkCopy crea una conexión dedicada, se habilitará una transacción.|False: no hay ninguna transacción|  
|int BatchSize|Número de filas en cada lote. Al final de cada lote, las filas del lote se envían al servidor.<br /><br /> Un lote estará completo cuando se hayan procesado las filas de BatchSize o no haya más filas para enviar al origen de datos de destino.  Si la instancia de SQLServerBulkCopy se ha declarado sin la opción UseInternalTransaction activa, las filas se envían a la vez a las filas de BatchSize del servidor pero no se realiza ninguna acción relacionada con la transacción. Si UseInternalTransaction está activa, cada lote de filas se inserta como una transacción independiente.|0: indica que cada operación writeToServer es un lote único|  
|Int BulkCopyTimeout|Cantidad de segundos para que se complete la operación antes de que se agote el tiempo de espera. Un valor de 0 indica sin límite; la copia masiva esperará indefinidamente.|60 segundos.|  
|Booleano allowEncryptedValueModifications|Esta opción está disponible con Microsoft JDBC Driver 6.0 (o superior) para SQL Server.<br /><br /> Cuando se especifica, **allowEncryptedValueModifications** permite la copia masiva de datos cifrados entre tablas o bases de datos, sin descifrar los datos. Normalmente, una aplicación puede seleccionar datos de las columnas cifradas de una tabla sin descifrar los datos (la aplicación debe conectarse a la base de datos con la palabra clave configuración de cifrado de columna establecida en deshabilitado) y, a continuación, use esta opción para los datos, una inserción masiva que sigue estando cifrado. Para obtener más información, consulte [usar Always Encrypted con el controlador JDBC](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).<br /><br /> Tenga precaución al especificar **allowEncryptedValueModifications** ya que puede provocar daños en la base de datos porque el controlador no comprueba si realmente se cifran los datos, o si se han cifrado correctamente mediante el mismo cifrado tipo, el algoritmo y la clave como la columna de destino.||  
  
 Captadores y establecedores:  
  
|Métodos|Description|  
|-------------|-----------------|  
|Booleano isCheckConstraints()|Indica si las restricciones deben comprobarse mientras se insertan los datos o no.|  
|Void setCheckConstraints(Boolean checkConstraints)|Establece si las restricciones deben comprobarse mientras se insertan los datos o no.|  
|Booleano isFireTriggers()|Indica si el servidor debe activar los desencadenadores de inserción para las filas que se va a insertar en la base de datos.|  
|Void setFireTriggers(Boolean fireTriggers)|Establece si el servidor debe establecerse en Activar desencadenadores para las filas que se va a insertar en la base de datos.|  
|Booleano isKeepIdentity()|Indica si se han de conservar los valores de identidad de origen o no.|  
|Void setKeepIdentity(Boolean keepIdentity)|Establece si desea conservar los valores de identidad o no.|  
|Booleano isKeepNulls()|Indica si se debe conservar valores null en la tabla de destino independientemente de la configuración para los valores predeterminados o si debe ser reemplazadas por los valores predeterminados (si procede).|  
|Void setKeepNulls(Boolean keepNulls)|Establece si se debe conservar valores null en la tabla de destino independientemente de la configuración para los valores predeterminados o si debe ser reemplazadas por los valores predeterminados (si procede).|  
|Booleano isTableLock()|Indica si SQLServerBulkCopy debe obtener un bloqueo de actualización masiva durante la operación de copia masiva.|  
|Void setTableLock(Boolean tableLock)|Establece si SQLServerBulkCopy debe obtener un bloqueo de actualización masiva durante la operación de copia masiva.|  
|Booleano isUseInternalTransaction()|Indica si se producirá cada lote de la operación de copia masiva en una transacción.|  
|Void setUseInternalTranscation(Boolean useInternalTransaction)|Establece si se producirá cada lote de las operaciones de copia masiva en una transacción o no.|  
|Int getBatchSize()|Obtiene el número de filas en cada lote. Al final de cada lote, las filas del lote se envían al servidor|  
|Void setBatchSize(int batchSize)|Establece el número de filas en cada lote. Al final de cada lote, las filas del lote se envían al servidor.|  
|Int getBulkCopyTimeout()|Obtiene el número de segundos para la operación se complete antes de que se agota el tiempo.|  
|Void setBulkCopyTimeout(int timeout)|Establece el número de segundos de la operación se complete antes de que se agota el tiempo.|  
|booleano isAllowEncryptedValueModifications()|Indica si la opción allowEncryptedValueModifications está habilitada o deshabilitada.|  
|void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)|Configura la configuración de allowEncryptedValueModifications que se usa para la copia masiva con columnas siempre cifradas.|  
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  
 La interfaz de ISQLServerBulkRecord se puede usar para crear las clases que leen datos de cualquier origen (como un archivo) y permite que una instancia de SQLServerBulkCopy cargue de forma masiva una tabla de SQL Server con esos datos.  
  
|Métodos de interfaz|Description|  
|-----------------------|-----------------|  
|Establecer\<entero > getColumnOrdinals()|Obtiene los ordinales para cada una de las columnas representadas en este registro de datos.|  
|Cadena getColumnName(int column)|Obtiene el nombre de una columna determinada.|  
|Int getColumnType (columna)|Obtiene el tipo de datos JDBC de la columna especificada.|  
|Int getPrecision (columna)|Obtiene la precisión de la columna especificada.|  
|Objeto getRowData()]|Obtiene los datos de la fila actual como una matriz de objetos.<br /><br /> Cada objeto debe coincidir con el tipo de lenguaje Java que se usa para representar el tipo de datos JDBC indicado para la columna especificada.  Para obtener más información, vea "Descripción de los tipos de datos del controlador JDBC" para las asignaciones adecuadas.|  
|Int getScale (columna)|Obtiene la escala de la columna especificada.|  
|Booleano Disautoincrement (columna)|Indica si la columna es representa una columna de identidad.|  
|Next() booleano|Avanza a la siguiente fila de datos.|  
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  
 Una implementación sencilla de la interfaz de ISQLServerBulkRecord que puede usarse para leer en los tipos de datos básicos de Java desde un archivo delimitado, donde cada línea representa una fila de datos.  
  
 Limitaciones y notas de implementación:  
  
1.  La cantidad máxima de datos permitida en una fila determinada está limitada por la memoria disponible, ya que los datos se leen en una línea cada vez.  
  
2.  No se admite la transmisión de tipos de datos de gran tamaño como varchar (max), varbinary (max), nvarchar (max), sqlxml, ntext.  
  
3.  El delimitador especificado para el archivo CSV no debe aparecer en ninguna parte de los datos y debe convertirse correctamente si es un carácter restringido en expresiones regulares de Java.  
  
4.  En la implementación del archivo CSV, las comillas dobles se tratan como parte de los datos. Por ejemplo, la línea hello, "world", "hello, world", si el delimitador es una coma, se tratará como si tuviera cuatro columnas con los valores de hello, "world", "hello y world".  
  
5.  Los caracteres de nueva línea se usan como terminadores de fila y no están permitidos en ninguna parte de los datos.  
  
|Constructor|Description|  
|-----------------|-----------------|  
|SQLServerBulkCSVFileRecord (fileToParse de cadena, cadena de codificación, delimitador de cadena, booleano firstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, String, String, boolean)|Inicializa una nueva instancia de la clase SQLServerBulkCSVFileRecord que analizará cada línea en el fileToParse con el delimitador y codificación proporcionados. Si firstLineIsColumnNames se establece en True, la primera línea del archivo se analizará como nombres de columna.  Si la codificación es NULL, se usará la codificación predeterminada.|  
|SQLServerBulkCSVFileRecord (fileToParse de cadena, cadena de codificación, booleano firstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, String, boolean)|Inicializa una nueva instancia de la clase SQLServerBulkCSVFileRecord que analizará cada línea en el fileToParse con la coma como delimitador y la codificación proporcionada. Si firstLineIsColumnNames se establece en True, la primera línea del archivo se analizará como nombres de columna.  Si la codificación es NULL, se usará la codificación predeterminada.|  
|SQLServerBulkCSVFileRecord (fileToParse de cadena, booleano firstLineIsColumnNamesSQLServerBulkCSVFileRecord (String, boolean)|Inicializa una nueva instancia de la clase SQLServerBulkCSVFileRecord que analizará cada línea en el fileToParse con la coma como delimitador y la codificación predeterminada. Si firstLineIsColumnNames se establece en True, la primera línea del archivo será will analizarse como nombres de columna.|  
  
|Método|Description|  
|------------|-----------------|  
|Void addColumnMetadata (int positionInFile, cadena columnName, jdbcType int, int precisión, escala de int)|Agrega metadatos de la columna especificada en el archivo.|  
|Close() void|Libera los recursos asociados con el lector de archivos.|  
|Void setTimestampWithTimezoneFormat (DateTim eFormatter dateTimeFormatter|Establece el formato para analizar los datos Timestamp desde el archivo como java.sql.Types.TIMESTAMP_WITH_TIMEZONE.|  
|Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter)|Establece el formato para analizar los datos Time desde el archivo como java.sql.Types.TIME_WITH_TIMEZONE.|  
|Void setTimeWithTimezoneFormat (DateTimeForm atter dateTimeFormatter)|Establece el formato para analizar los datos Time desde el archivo como java.sql.Types.TIME_WITH_TIMEZONE.|  
|Void setTimeWithTimezoneFormat(String timeFormat)|Establece el formato para analizar los datos Time desde el archivo como java.sql.Types.TIME_WITH_TIMEZONE.|  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
