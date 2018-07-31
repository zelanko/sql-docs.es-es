---
title: Usar parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4852b9d6546375246c9236ccdfb8522c00ec548a
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279216"
---
# <a name="using-table-valued-parameters"></a>Usar parámetros con valores de tabla
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla puede operar utilizando Transact-SQL.  
  
 Valores de columna de parámetros con valores de tabla se pueden acceder mediante instrucciones estándar SELECT de Transact-SQL. Parámetros con valores de tabla están fuertemente tipados y su estructura se valida automáticamente. El tamaño de los parámetros con valores de tabla está limitado únicamente por la memoria de servidor.  
  
> [!NOTE]  
>  Compatibilidad con parámetros con valores de tabla está disponible a partir de Microsoft JDBC Driver 6.0 para SQL Server.  
  
> [!NOTE]  
>  No se puede devolver datos en un parámetro con valores de tabla. Parámetros con valores de tabla son sólo de entrada; no se admite la palabra clave OUTPUT.  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|--------------|-----------------|  
|[Parámetros con valores de tabla (motor de base de datos)](http://go.microsoft.com/fwlink/?LinkId=98363) en los libros en pantalla de SQL Server|Describe cómo crear y usar parámetros con valores de tabla|  
|[Tipos de tabla definido por el usuario](http://go.microsoft.com/fwlink/?LinkId=98364) en los libros en pantalla de SQL Server|Describe los tipos de tabla definido por el usuario que se usan para declarar parámetros con valores de tabla|  
|El [motor de base de datos de Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=120507) sección de CodePlex|Contiene ejemplos que muestran cómo usar la funcionalidad y características de SQL Server|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Pasar varias filas en las versiones anteriores de SQL Server  
 Antes de que los parámetros con valores de tabla se introdujeron en SQL Server 2008, las opciones para pasar varias filas de datos a un procedimiento almacenado o un comando SQL con parámetros eran limitadas. Un programador podía elegir entre las siguientes opciones para pasar varias filas en el servidor:  
  
-   Usar una serie de parámetros individuales para representar los valores en varias columnas y filas de datos. La cantidad de datos que se pueden pasar mediante este método está limitada por el número de parámetros permitidos. Procedimientos de SQL Server pueden tener, como máximo, 2100 parámetros. Lógica de servidor es necesario para ensamblar estos valores individuales en una variable de tabla o una tabla temporal para su procesamiento.  
  
-   Agrupar varios valores de datos en cadenas delimitadas o documentos XML y, a continuación, pasar los valores de texto a un procedimiento o instrucción. Esto requiere el procedimiento o la instrucción para incluir la lógica necesaria para validar las estructuras de datos y desempaquetar los valores.  
  
-   Crear una serie de instrucciones SQL individuales para las modificaciones de datos que afectan a varias filas. Los cambios pueden ser enviados al servidor individualmente o por lotes en grupos. Sin embargo, aunque se envíen por lotes que contengan varias instrucciones, cada instrucción se ejecuta por separado en el servidor.  
  
-   Usar el programa de utilidad bcp o la [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) objeto para cargar muchas filas de datos en una tabla. Aunque esta técnica es muy eficaz, no es compatible con el procesamiento de servidor a menos que se cargan los datos en una tabla temporal o una variable de tabla.  
  
## <a name="creating-table-valued-parameter-types"></a>Creación de tipos de parámetro con valores de tabla  
 Parámetros con valores de tabla se basan en estructuras de tabla fuertemente tipadas definidas mediante instrucciones CREATE TYPE de Transact-SQL. Tendrá que crear un tipo de tabla y definir la estructura en SQL Server para poder usar parámetros con valores de tabla en las aplicaciones cliente. Para obtener más información acerca de cómo crear tipos de tabla, vea [tipos de tabla definidos por el usuario](http://go.microsoft.com/fwlink/?LinkID=98364) en libros en pantalla de SQL Server.  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 Después de crear un tipo de tabla, puede declarar parámetros con valores de tabla en función de ese tipo. El siguiente fragmento de Transact-SQL muestra cómo declarar un parámetro con valores de tabla en una definición de procedimiento almacenado. Tenga en cuenta que la palabra clave READONLY se requiere para declarar un parámetro con valores de tabla.  
  
```sql
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modificación de datos con parámetros con valores de tabla (Transact-SQL)  
 Parámetros con valores de tabla se pueden usar en modificaciones basadas en conjuntos de datos que afectan a varias filas mediante la ejecución de una sola instrucción. Por ejemplo, puede seleccionar todas las filas en un parámetro con valores de tabla e insertarlas en una tabla de base de datos, o puede crear una instrucción update mediante la combinación de un parámetro con valores de tabla a la tabla que desea actualizar.  
  
 La siguiente instrucción UPDATE de Transact-SQL muestra cómo usar un parámetro con valores de tabla mediante su unión con la tabla Categories. Cuando se usa un parámetro con valores de tabla con una combinación en una cláusula FROM, debe también alias, como se muestra aquí, donde el parámetro con valores de tabla es un alias "EC":  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 En este ejemplo de Transact-SQL muestra cómo seleccionar las filas de un parámetro con valores de tabla para realizar una INSERCIÓN en una sola operación basada en conjunto.  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>Limitaciones de los parámetros con valores de tabla  
 Existen varias limitaciones a los parámetros con valores de tabla:  
  
-   No se puede pasar parámetros con valores de tabla a las funciones definidas por el usuario.  
  
-   Parámetros con valores de tabla solo se pueden indizar para admitir restricciones UNIQUE o PRIMARY KEY. SQL Server no mantiene estadísticas en los parámetros con valores de tabla.  
  
-   Parámetros con valores de tabla son de solo lectura en el código de Transact-SQL. No se puede actualizar los valores de columna en las filas de un parámetro con valores de tabla y no se puede insertar o eliminar filas. Para modificar los datos que se pasan a un procedimiento almacenado o instrucción en el parámetro con valores de tabla con parámetros, debe insertar los datos en una tabla temporal o en una variable de tabla.  
  
-   No se puede usar instrucciones ALTER TABLE para modificar el diseño de parámetros con valores de tabla.
-   Puede transmitir objetos grandes en un parámetro con valores de tabla.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configuración de un parámetro con valores de tabla  
 Desde Microsoft JDBC Driver 6.0 para SQL Server, se admiten parámetros con valores de tabla con una instrucción con parámetros o un procedimiento almacenado con parámetros. Parámetros con valores de tabla se rellena a partir de un SQLServerDataTable, desde un conjunto de resultados o de un usuario proporciona la implementación de la interfaz ISQLServerDataRecord. Al establecer un parámetro con valores de tabla para una consulta preparada, debe especificar un nombre de tipo que debe coincidir con el nombre de un tipo compatible previamente creado en el servidor.  
  
 Los siguientes dos fragmentos de código muestran cómo configurar un parámetro con valores de tabla con SQLServerPreparedStatement y con un SQLServerCallableStatement para insertar datos. Aquí puede ser sourceTVPObject un SQLServerDataTable, o un conjunto de resultados o un objeto ISQLServerDataRecord. Los ejemplos se supone la conexión es un objeto de conexión activo.  
  
```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =   
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```  
  
```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =   
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");       
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de API disponibles para el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Pasar un parámetro con valores de tabla como un objeto SQLServerDataTable  
 Desde Microsoft JDBC Driver 6.0 para SQL Server, la clase SQLServerDataTable representa una tabla en memoria de datos relacionales. En este ejemplo se muestra cómo construir un parámetro con valores de tabla de datos en memoria mediante el objeto SQLServerDataTable. En primer lugar, el código crea un objeto SQLServerDataTable, define su esquema y rellena la tabla con datos. El código, a continuación, configura SQLServerPreparedStatement que esta tabla de datos que se pasa como un parámetro con valores de tabla a SQL Server.  
  
```java
// Assumes connection is an active Connection object.  
  
// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();   
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);   
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);   
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");   
sourceDataTable.addRow(2, "CategoryNameValue2");   
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =   
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de API disponibles para el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Pasar un parámetro con valores de tabla como un objeto de conjunto de resultados  
 En este ejemplo se muestra cómo transmitir filas de datos de un conjunto de resultados a un parámetro con valores de tabla. El código primero recupera datos de una tabla de origen en un crea un objeto SQLServerDataTable, define su esquema y rellena la tabla con datos. El código, a continuación, configura SQLServerPreparedStatement que esta tabla de datos que se pasa como un parámetro con valores de tabla a SQL Server.  
  
```java
// Assumes connection is an active Connection object.  
  
// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.   
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  
  
// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =   
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de API disponibles para el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Pasar un parámetro con valores de tabla como un objeto ISQLServerDataRecord  
 Desde Microsoft JDBC Driver 6.0 para SQL Server, una nueva interfaz ISQLServerDataRecord está disponible para la transmisión de datos (dependiendo de cómo el usuario proporciona la implementación para él) con un parámetro con valores de tabla. En el ejemplo siguiente se muestra cómo implementar la interfaz ISQLServerDataRecord y pasarlo como un parámetro con valores de tabla. Por motivos de simplicidad, el siguiente ejemplo pasa una sola fila con valores codificados de forma rígida para el parámetro con valores de tabla. Idealmente, el usuario debería implementar esta interfaz para transmitir filas de cualquier origen, por ejemplo, de archivos de texto.  
  
```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.   
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;       
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }     
}  
  
// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =   
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de API disponibles para el parámetro con valores de tabla.  
    
## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>API de parámetro con valores de tabla para el controlador JDBC  
 **SQLServerMetaData**  
  
 Esta clase representa los metadatos para una columna. Se utiliza en la interfaz ISQLServerDataRecord para pasar los metadatos de columna para el parámetro con valores de tabla. Los métodos de esta clase son:  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerMetaData pública (cadena columnName, sqlType int, int precisión, escala de int, useServerDefault booleano, isUniqueKey booleano, sortOrder SQLServerSortOrder, sortOrdinal int)|Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna especificado, tipo sql, precisión, escala y el servidor predeterminado. Este formulario del constructor admite parámetros con valores de tabla, ya que permite especificar si la columna es única en el parámetro con valores de tabla, el criterio de ordenación para la columna y el ordinal de la columna de ordenación. <br><br>useServerDefault: Especifica si esta columna debe usar el valor predeterminado del servidor; Valor predeterminado es false.<br>isUniqueKey - indica si la columna en el parámetro con valores de tabla es única; Valor predeterminado es false.<br>sortOrder - indica el criterio de ordenación de una columna: Valor predeterminado es SQLServerSortOrder.Unspecified.<br>sortOrdinal: especifica el ordinal de la columna de ordenación sortOrdinal comienza desde 0. Valor predeterminado es -1.|
|SQLServerMetaData pública (cadena columnName, sqlType int)|Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna y el tipo sql.|  
|SQLServerMetaData pública (cadena columnName, sqlType int, int precisión, escala int)|Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna, tipo de sql, precisión y escala.|  
|SQLServerMetaData pública (SQLServerMetaData sqlServerMetaData)|Inicializa una nueva instancia de SQLServerMetaData desde otro objeto SQLServerMetaData.|  
|getColumName() de cadena pública|Recupera el nombre de columna.|  
|getSqlType() int pública|Recupera el tipo sql de java.|  
|getPrecision() int pública|Recupera la precisión del tipo pasado a la columna.|  
|getScale() int pública|Recupera la escala del tipo pasado a la columna.|  
|pública getSortOrder() SQLServerSortOrder|Recupera el criterio de ordenación.|
|getSortOrdinal() int pública|Recupera el ordinal de ordenación.|
|pública isUniqueKey() booleano|Devuelve si la columna es única.|
|pública useServerDefault() booleano|Wheher devuelve la columna utiliza el valor predeterminado del servidor.|
  
 **SQLServerSortOrder**
 
 Una enumeración que define el criterio de ordenación. Los valores posibles son Ascending, Descending y no especificado. 
  
 **SQLServerDataTable**  
  
 Esta clase representa una tabla de datos en memoria para su uso con parámetros con valores de tabla. Los métodos de esta clase son:  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerDataTable() pública|Inicializa una nueva instancia de SQLServerDataTable.|  
|Iterador públicos < entrada\<entero, Object [] >> getIterator()|Recupera un iterador en las filas de la tabla de datos.|  
|public void addColumnMetadata (cadena columnName, sqlType int)|Agrega metadatos de la columna especificada.|  
|addColumnMetadata void público (columna SQLServerDataColumn)|Agrega metadatos de la columna especificada.|  
|addRow void público (objeto... valores)|Agrega una fila de datos a la tabla de datos.|  
|Mapa pública\<entero, SQLServerDataColumn > getColumnMetadata()|Recupera metadatos de columna de esta tabla de datos.|
|clear() void público |Borra esta tabla de datos. |  
  
 **SQLServerDataColumn**  
  
 Esta clase representa una columna de la tabla de datos en memoria representada por SQLServerDataTable. Los métodos de esta clase son:  
  
|Nombre|Descripción|  
|----------|-----------------|  
|SQLServerDataColumn pública (cadena columnName, sqlType int)|Inicializa una nueva instancia de SQLServerDataColumn con el nombre de columna y el tipo.|  
|getColumnName() de cadena pública|Recupera el nombre de columna.|  
|getColumnType() int pública|Recupera el tipo de columna.|  
  
 **ISQLServerDataRecord**  
  
 Esta clase representa una interfaz que los usuarios pueden implementar para transmitir datos a un parámetro con valores de tabla. Los métodos de esta interfaz son:  
  
|Nombre|Descripción|  
|----------|-----------------|  
|pública SQLServerMetaData getColumnMetaData (columna int);|Recupera los metadatos de columna del índice de columna especificado.|  
|getColumnCount() int pública;|Recupera el número total de columnas.|  
|getRowData() de [] objeto pública;|Recupera los datos de la fila actual como una matriz de objetos.|  
|next() booleano pública;|Se desplaza a la siguiente fila. Devuelve True si el movimiento es correcto y no hay una fila siguiente, false en caso contrario.|  
  
 **SQLServerPreparedStatement**  
  
 Los métodos siguientes se agregaron a esta clase para admitir la transmisión de parámetros con valores de tabla.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|final setStructured void público (parameterIndex int, String tvpName, SQLServerDataTable tvpDataTbale)|Rellena un parámetro con valores de tabla con una tabla de datos. parameterIndex es el índice del parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpDataTable es el objeto de tabla de datos de origen.|  
|final setStructured void público (parameterIndex int, String tvpName, ResultSet tvpResultSet)|Un parámetro con valores de tabla se rellena con un conjunto de resultados recuperado de la tabla de otro. parameterIndex es el índice del parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpResultSet es el objeto de conjunto de resultados de origen.|  
|final setStructured void público (parameterIndex int, String tvpName, ISQLServerDataRecord tvpDataRecord)|Rellena un parámetro con valores de tabla con un objeto ISQLServerDataRecord. ISQLServerDataRecord se usa para transmitir datos y el usuario decide cómo se usa. parameterIndex es el índice del parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpDataRecord es un objeto ISQLServerDataRecord.|  
  
 **SQLServerCallableStatement**  
  
 Los métodos siguientes se agregaron a esta clase para admitir la transmisión de parámetros con valores de tabla.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|final setStructured void público (paratemeterName de cadena, cadena tvpName, SQLServerDataTable tvpDataTable)|Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con una tabla de datos. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpDataTable es el objeto de tabla de datos.|  
|final setStructured void público (paratemeterName de cadena, cadena tvpName, ResultSet tvpResultSet)|Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con un conjunto de resultados recuperado de otra tabla. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpResultSet es el objeto de conjunto de resultados de origen.|  
|final setStructured void público (paratemeterName de cadena, cadena tvpName, ISQLServerDataRecord tvpDataRecord)|Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con un objeto ISQLServerDataRecord. ISQLServerDataRecord se usa para transmitir datos y el usuario decide cómo se usa. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpDataRecord es un objeto ISQLServerDataRecord.|  
  
## <a name="see-also"></a>Ver también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
