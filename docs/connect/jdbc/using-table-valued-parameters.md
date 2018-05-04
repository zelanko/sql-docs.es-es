---
title: Usar parámetros con valores de tabla | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6ac7155299100c0faecae67c8d8465a11305e26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-table-valued-parameters"></a>Usar parámetros con valores de tabla
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Los parámetros con valores de tabla proporcionan una manera fácil de serializar varias filas de datos desde una aplicación cliente a SQL Server sin necesidad de varios viajes de ida y vuelta o lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos de entrada se almacenan en una variable de tabla que, a continuación, puede tratarse mediante Transact-SQL.  
  
 Pueden tener acceso a los valores de columna de parámetros con valores de tabla mediante instrucciones estándares SELECT de Transact-SQL. Parámetros con valores de tabla están fuertemente tipados y su estructura se valida automáticamente. El tamaño de los parámetros con valores de tabla está limitado únicamente por la memoria de servidor.  
  
> [!NOTE]  
>  Compatibilidad con parámetros con valores de tabla está disponible a partir de Microsoft JDBC Driver 6.0 para SQL Server.  
  
> [!NOTE]  
>  No puede devolver datos en un parámetro con valores de tabla. Parámetros con valores de tabla son sólo de entrada; no se admite la palabra clave OUTPUT.  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea los siguientes recursos.  
  
|Recurso|Description|  
|--------------|-----------------|  
|[Parámetros con valores de tabla (motor de base de datos)](http://go.microsoft.com/fwlink/?LinkId=98363) en libros en pantalla de SQL Server|Describe cómo crear y usar parámetros con valores de tabla|  
|[Tipos de tabla definidos por el usuario](http://go.microsoft.com/fwlink/?LinkId=98364) en libros en pantalla de SQL Server|Describe los tipos de tabla definidos por el usuario que se usan para declarar parámetros con valores de tabla|  
|El [motor de base de datos de Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=120507) sección de CodePlex|Contiene ejemplos que muestran cómo utilizar la funcionalidad y las características de SQL Server|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Pasar varias filas en las versiones anteriores de SQL Server  
 Antes de que los parámetros con valores de tabla se introdujeron en SQL Server 2008, las opciones para pasar varias filas de datos a un procedimiento almacenado o un comando SQL con parámetros eran limitadas. Un programador podía elegir entre las siguientes opciones para pasar varias filas en el servidor:  
  
-   Usar una serie de parámetros individuales para representar los valores de varias columnas y filas de datos. La cantidad de datos que se pueden pasar mediante este método está limitada por el número de parámetros permitidos. Procedimientos de SQL Server pueden tener, como máximo, 2100 parámetros. Lógica de servidor es necesario para ensamblar estos valores individuales en una variable de tabla o una tabla temporal para su procesamiento.  
  
-   Agrupar varios valores de datos en cadenas delimitadas o documentos XML y, a continuación, pasar esos valores de texto a un procedimiento o una instrucción. Esto requiere el procedimiento o una instrucción para incluir la lógica necesaria para validar las estructuras de datos y desempaquetar los valores.  
  
-   Crear una serie de instrucciones SQL individuales para las modificaciones de datos que afectan a varias filas. Pueden ser enviados al servidor de forma individual o por lotes en grupos de cambios. Sin embargo, aunque se envíen por lotes que contengan varias instrucciones, cada instrucción se ejecuta por separado en el servidor.  
  
-   Usar el programa de la utilidad bcp o la [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) objeto que se va a cargar muchas filas de datos en una tabla. Aunque esta técnica es muy eficaz, no es compatible con procesamiento de servidor a menos que se cargan los datos en una tabla temporal o una variable de tabla.  
  
## <a name="creating-table-valued-parameter-types"></a>Creación de tipos de parámetro con valores de tabla  
 Parámetros con valores de tabla se basan en estructuras de tabla fuertemente tipada que se definen mediante instrucciones Transact-SQL CREATE TYPE. Tendrá que crear un tipo de tabla y definir la estructura en SQL Server para poder usar parámetros con valores de tabla en las aplicaciones cliente. Para obtener más información acerca de cómo crear tipos de tabla, vea [tipos de tabla definidos por el usuario](http://go.microsoft.com/fwlink/?LinkID=98364) en libros en pantalla de SQL Server.  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 Después de crear un tipo de tabla, puede declarar parámetros con valores de tabla en función de ese tipo. El fragmento de Transact-SQL siguiente muestra cómo declarar un parámetro con valores de tabla en una definición de procedimiento almacenado. Tenga en cuenta que la palabra clave READONLY para declarar un parámetro con valores de tabla.  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modificar datos con parámetros con valores de tabla (Transact-SQL)  
 Parámetros con valores de tabla pueden utilizarse en las modificaciones de datos basadas en conjuntos que afectan a varias filas mediante la ejecución de una sola instrucción. Por ejemplo, puede seleccionar todas las filas en un parámetro con valores de tabla e insertarlos en una tabla de base de datos, o puede crear una instrucción update mediante la combinación de un parámetro con valores de tabla a la tabla que desea actualizar.  
  
 La siguiente instrucción UPDATE de Transact-SQL muestra cómo usar un parámetro con valores de tabla en combinación con la tabla Categories. Cuando se usa un parámetro con valores de tabla con una combinación en una cláusula FROM, debe asignarle un alias, como se muestra aquí, donde el parámetro con valores de tabla es un alias "EC":  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 En este ejemplo de Transact-SQL se muestra cómo seleccionar filas de un parámetro con valores de tabla para realizar una INSERCIÓN en una sola operación basada en conjunto.  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>Limitaciones de los parámetros con valores de tabla  
 Existen varias limitaciones a los parámetros con valores de tabla:  
  
-   No se puede pasar parámetros con valores de tabla a las funciones definidas por el usuario.  
  
-   Parámetros con valores de tabla solo se pueden indizar para admitir restricciones UNIQUE o PRIMARY KEY. SQL Server no mantiene estadísticas en parámetros con valores de tabla.  
  
-   Parámetros con valores de tabla son de solo lectura en el código de Transact-SQL. No se puede actualizar los valores de columna en las filas de un parámetro con valores de tabla y no se puede insertar o eliminar filas. Para modificar los datos que se pasan a un procedimiento almacenado o instrucción de parámetro con valores de tabla con parámetros, debe insertar los datos en una tabla temporal o en una variable de tabla.  
  
-   No se puede usar instrucciones ALTER TABLE para modificar el diseño de los parámetros con valores de tabla.
-   Puede transmitir objetos grandes en un parámetro con valores de tabla.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configuración de un parámetro con valores de tabla  
 Desde Microsoft JDBC Driver 6.0 para SQL Server, se admiten parámetros con valores de tabla con una instrucción con parámetros o un procedimiento almacenado con parámetros. Parámetros con valores de tabla se rellena a partir de un SQLServerDataTable, de un conjunto de resultados o de un usuario proporciona la implementación de la interfaz ISQLServerDataRecord. Al establecer un parámetro con valores de tabla para una consulta preparada, debe especificar un nombre de tipo que debe coincidir con el nombre de un tipo compatible previamente creado en el servidor.  
  
 Los siguientes dos fragmentos de código muestran cómo configurar un parámetro con valores de tabla con SQLServerPreparedStatement y con un SQLServerCallableStatement para insertar datos. Aquí sourceTVPObject puede ser un SQLServerDataTable, o un conjunto de resultados o un objeto ISQLServerDataRecord. Los ejemplos se supone conexión es un objeto de conexión activo.  
  
```  
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =   
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```  
  
```  
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =   
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");       
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```  
  
> [!NOTE]  
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de las API disponibles para configurar el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Pasar un parámetro con valores de tabla como un objeto SQLServerDataTable  
 Comenzar con Microsoft JDBC Driver 6.0 para SQL Server, la clase SQLServerDataTable representa una tabla en memoria de datos relacionales. Este ejemplo muestra cómo construir un parámetro con valores de tabla de datos en memoria utilizando el objeto SQLServerDataTable. En primer lugar, el código crea un objeto SQLServerDataTable, define su esquema y rellena la tabla con datos. El código, a continuación, configura un SQLServerPreparedStatement que esta tabla de datos que se pasa como un parámetro con valores de tabla en SQL Server.  
  
```  
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
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de las API disponibles para configurar el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Pasar un parámetro con valores de tabla como un objeto de conjunto de resultados  
 Este ejemplo muestra cómo transmitir por secuencias filas de datos de un conjunto de resultados a un parámetro con valores de tabla. El código primero recupera datos de una tabla de origen en un crea un objeto SQLServerDataTable, define su esquema y rellena la tabla con datos. El código, a continuación, configura un SQLServerPreparedStatement que esta tabla de datos que se pasa como un parámetro con valores de tabla en SQL Server.  
  
```  
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
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de las API disponibles para configurar el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Pasar un parámetro con valores de tabla como un objeto ISQLServerDataRecord  
 Comenzar con Microsoft JDBC Driver 6.0 para SQL Server, una nueva interfaz ISQLServerDataRecord está disponible para la transmisión de datos (en función de cómo el usuario proporciona la implementación para él) con un parámetro con valores de tabla. En el ejemplo siguiente se muestra cómo implementar la interfaz ISQLServerDataRecord y cómo pasar como un parámetro con valores de tabla. Para simplificar, en el ejemplo siguiente se pasa una sola fila con valores codificados de forma rígida para el parámetro con valores de tabla. Idealmente, el usuario debería implementar esta interfaz para transmitir filas de cualquier origen, por ejemplo archivos de texto.  
  
```  
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
>  Consulte la sección **API de parámetro con valores de tabla para el controlador JDBC** a continuación para obtener una lista completa de las API disponibles para configurar el parámetro con valores de tabla.  
    
## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>API de parámetro con valores de tabla para el controlador JDBC  
 **SQLServerMetaData**  
  
 Esta clase representa los metadatos para una columna. Se usa en la interfaz ISQLServerDataRecord para pasar metadatos de columna para el parámetro con valores de tabla. Los métodos de esta clase son:  
  
|Nombre|Description|  
|----------|-----------------|  
|SQLServerMetaData pública (cadena columnName, sqlType int, int precisión, escala de int, useServerDefault booleano, isUniqueKey booleano, SQLServerSortOrder sortOrder, sortOrdinal int)|Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna especificado, tipo de sql, precisión, escala y el servidor predeterminado. Este formulario del constructor es compatible con parámetros con valores de tabla, por lo que le permite especificar si la columna es única en el parámetro con valores de tabla, el criterio de ordenación para la columna y el ordinal de la columna de ordenación. <br><br>useServerDefault - especifica si esta columna debe usar el valor de servidor predeterminado; Valor predeterminado es false.<br>isUniqueKey - indica si la columna en el parámetro con valores de tabla es única; Valor predeterminado es false.<br>sortOrder - indica el criterio de ordenación para una columna; Valor predeterminado es SQLServerSortOrder.Unspecified.<br>sortOrdinal - especifica el ordinal de la columna de ordenación; sortOrdinal se inicia en 0; Valor predeterminado es -1.|
|SQLServerMetaData pública (cadena columnName, sqlType int)|Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna y el tipo de sql.|  
|SQLServerMetaData pública (cadena columnName, sqlType int, int precisión, escala de int)|Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna, tipo de sql, precisión y escala.|  
|SQLServerMetaData pública (SQLServerMetaData sqlServerMetaData)|Inicializa una nueva instancia de SQLServerMetaData desde otro objeto SQLServerMetaData.|  
|getColumName() de cadena pública|Recupera el nombre de columna.|  
|int pública getSqlType()|Recupera el tipo sql de java.|  
|int pública getPrecision()|Recupera la precisión del tipo pasado a la columna.|  
|int pública getScale()|Recupera la escala del tipo pasado a la columna.|  
|pública getSortOrder() SQLServerSortOrder|Recupera el criterio de ordenación.|
|int pública getSortOrdinal()|Recupera el ordinal de la ordenación.|
|pública isUniqueKey() booleano|Devuelve si la columna es única.|
|pública useServerDefault() booleano|Wheher devuelve la columna utiliza el valor de servidor predeterminado.|
  
 **SQLServerSortOrder**
 
 Una enumeración que define el criterio de ordenación. Los valores posibles son ascendente, descendente y no especificado. 
  
 **SQLServerDataTable**  
  
 Esta clase representa una tabla de datos en memoria para su uso con parámetros con valores de tabla. Los métodos de esta clase son:  
  
|Nombre|Description|  
|----------|-----------------|  
|SQLServerDataTable() público|Inicializa una nueva instancia de SQLServerDataTable.|  
|Iterador pública < entrada\<entero, Object [] >> getIterator()|Recupera un iterador en las filas de la tabla de datos.|  
|public void addColumnMetadata (cadena columnName, sqlType int)|Agrega metadatos para la columna especificada.|  
|addColumnMetadata void público (columna SQLServerDataColumn)|Agrega metadatos para la columna especificada.|  
|pública addRow void (objeto... valores)|Agrega una fila de datos a la tabla de datos.|  
|Mapa pública\<entero, SQLServerDataColumn > getColumnMetadata()|Recupera los metadatos de columna de esta tabla de datos.|
|pública clear() void |Borra esta tabla de datos. |  
  
 **SQLServerDataColumn**  
  
 Esta clase representa una columna de la tabla de datos en memoria representada por SQLServerDataTable. Los métodos de esta clase son:  
  
|Nombre|Description|  
|----------|-----------------|  
|SQLServerDataColumn pública (cadena columnName, sqlType int)|Inicializa una nueva instancia de SQLServerDataColumn con el nombre de columna y el tipo.|  
|getColumnName() de cadena pública|Recupera el nombre de columna.|  
|int pública getColumnType()|Recupera el tipo de columna.|  
  
 **ISQLServerDataRecord**  
  
 Esta clase representa una interfaz que los usuarios pueden implementar para transmitir datos a un parámetro con valores de tabla. Los métodos en esta interfaz son:  
  
|Nombre|Description|  
|----------|-----------------|  
|pública SQLServerMetaData getColumnMetaData (columna);|Recupera los metadatos de columna del índice de columna determinado.|  
|getColumnCount() int pública;|Recupera el número total de columnas.|  
|pública objeto [] getRowData();|Recupera los datos de la fila actual como una matriz de objetos.|  
|pública next() booleano;|Se desplaza a la siguiente fila. Devuelve True si el movimiento es correcto y no hay una fila siguiente, false en caso contrario.|  
  
 **SQLServerPreparedStatement**  
  
 Se agregaron los siguientes métodos para esta clase para admitir el paso de parámetros con valores de tabla.  
  
|Nombre|Description|  
|----------|-----------------|  
|pública setStructured void final (parameterIndex int, String tvpName, SQLServerDataTable tvpDataTbale)|Rellena un parámetro con valores de tabla con una tabla de datos. parameterIndex es el índice de parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpDataTable es el objeto de tabla de datos de origen.|  
|pública setStructured void final (parameterIndex int, cadena tvpName, ResultSet tvpResultSet)|Un parámetro con valores de tabla se rellena con un conjunto de resultados recuperado de otra tabla. parameterIndex es el índice de parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpResultSet es el objeto de conjunto de resultados de origen.|  
|pública setStructured void final (parameterIndex int, String tvpName, ISQLServerDataRecord tvpDataRecord)|Rellena un parámetro con valores de tabla con un objeto ISQLServerDataRecord. ISQLServerDataRecord se utiliza para la transmisión de datos y el usuario decide cómo utilizarla. parameterIndex es el índice de parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpDataRecord es un objeto ISQLServerDataRecord.|  
  
 **SQLServerCallableStatement**  
  
 Se agregaron los siguientes métodos para esta clase para admitir el paso de parámetros con valores de tabla.  
  
|Nombre|Description|  
|----------|-----------------|  
|pública setStructured void final (paratemeterName de cadena, cadena tvpName, SQLServerDataTable tvpDataTable)|Rellena un parámetro con valores de tabla pasado a un procedimiento almacenado con una tabla de datos. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpDataTable es el objeto de tabla de datos.|  
|pública setStructured void final (paratemeterName de cadena, cadena tvpName, ResultSet tvpResultSet)|Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con un conjunto de resultados recuperado de otra tabla. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpResultSet es el objeto de conjunto de resultados de origen.|  
|pública setStructured void final (paratemeterName de cadena, cadena tvpName, ISQLServerDataRecord tvpDataRecord)|Rellena un parámetro con valores de tabla pasado a un procedimiento almacenado con un objeto ISQLServerDataRecord. ISQLServerDataRecord se utiliza para la transmisión de datos y el usuario decide cómo utilizarla. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpDataRecord es un objeto ISQLServerDataRecord.|  
  
## <a name="see-also"></a>Vea también  
 [Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
