---
title: Usar parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cd5f00d551c189f583af4232fe31716b51594df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003925"
---
# <a name="using-table-valued-parameters"></a>Usar parámetros con valores de tabla

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla en la que, a continuación, se puede operar mediante el uso de Transact-SQL.  
  
Se puede tener acceso a los valores de columna de los parámetros con valores de tabla mediante instrucciones SELECT de Transact-SQL estándar. Los parámetros con valores de tabla están fuertemente tipados y su estructura se valida automáticamente. El tamaño de los parámetros con valores de tabla solo está limitado por la memoria del servidor.  
  
> [!NOTE]  
> La compatibilidad con los parámetros con valores de tabla está disponible a partir de Microsoft JDBC driver 6,0 para SQL Server.
>
> No se pueden devolver datos en un parámetro con valores de tabla. Los parámetros con valores de tabla son de solo entrada; no se admite la palabra clave OUTPUT.  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea los siguientes recursos.  
  
| Recurso                                                                                                             | Descripción                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [Parámetros con valores de tabla (motor de base de datos)](https://go.microsoft.com/fwlink/?LinkId=98363) en libros en pantalla de SQL Server | Describe cómo crear y usar parámetros con valores de tabla.                             |
| [Tipos de tabla definidos por el usuario](https://go.microsoft.com/fwlink/?LinkId=98364) en libros en pantalla de SQL Server                  | Describe los tipos de tabla definidos por el usuario que se usan para declarar parámetros con valores de tabla. |
| La sección [Microsoft SQL Server motor de base de datos](https://go.microsoft.com/fwlink/?LinkId=120507) de CodePlex        | Contiene ejemplos que muestran cómo usar las características y la funcionalidad de SQL Server  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Pasar varias filas en versiones anteriores de SQL Server  

Antes de que los parámetros con valores de tabla se introdujeron en SQL Server 2008, las opciones para pasar varias filas de datos a un procedimiento almacenado o a un comando SQL con parámetros eran limitadas. Un desarrollador podría elegir entre las siguientes opciones para pasar varias filas al servidor:  
  
- Use una serie de parámetros individuales para representar los valores de varias columnas y filas de datos. La cantidad de datos que se pueden pasar mediante este método está limitada por el número de parámetros permitidos. SQL Server procedimientos pueden tener, como máximo, 2100 parámetros. La lógica del lado servidor es necesaria para ensamblar estos valores individuales en una variable de tabla o una tabla temporal para su procesamiento.  
  
- Agrupar varios valores de datos en cadenas delimitadas o documentos XML y, a continuación, pasar esos valores de texto a un procedimiento o instrucción. Esto requiere que el procedimiento o la instrucción incluyan la lógica necesaria para validar las estructuras de datos y desagrupar los valores.  
  
- Cree una serie de instrucciones SQL individuales para las modificaciones de datos que afecten a varias filas. Los cambios se pueden enviar al servidor individualmente o por lotes en grupos. Sin embargo, incluso cuando se envían en lotes que contienen varias instrucciones, cada instrucción se ejecuta por separado en el servidor.  
  
- Use el programa de la utilidad BCP o el objeto [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) para cargar muchas filas de datos en una tabla. Aunque esta técnica es muy eficaz, no admite el procesamiento del lado servidor a menos que los datos se carguen en una tabla temporal o una variable de tabla.  
  
## <a name="creating-table-valued-parameter-types"></a>Crear tipos de parámetro con valores de tabla  

Los parámetros con valores de tabla se basan en estructuras de tabla fuertemente tipadas definidas mediante instrucciones Transact-SQL `CREATE TYPE` . Debe crear un tipo de tabla y definir la estructura en SQL Server antes de poder usar parámetros con valores de tabla en las aplicaciones cliente. Para obtener más información sobre la creación de tipos de tabla, vea [tipos de tabla definidos por el usuario](https://go.microsoft.com/fwlink/?LinkID=98364) en libros en pantalla de SQL Server.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

Después de crear un tipo de tabla, puede declarar parámetros con valores de tabla basados en ese tipo. El siguiente fragmento de Transact-SQL muestra cómo declarar un parámetro con valores de tabla en una definición de procedimiento almacenado. Tenga en cuenta `READONLY` que la palabra clave es necesaria para declarar un parámetro con valores de tabla.  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modificar datos con parámetros con valores de tabla (Transact-SQL)  

Los parámetros con valores de tabla se pueden utilizar en las modificaciones de datos basadas en conjuntos que afectan a varias filas mediante la ejecución de una única instrucción. Por ejemplo, puede seleccionar todas las filas de un parámetro con valores de tabla e insertarlas en una tabla de base de datos, o puede crear una instrucción UPDATE combinando un parámetro con valores de tabla en la tabla que desea actualizar.  
  
La siguiente instrucción UPDATE de Transact-SQL muestra cómo usar un parámetro con valores de tabla mediante su combinación con la tabla Categories. Cuando se usa un parámetro con valores de tabla con una combinación en una cláusula FROM, también se debe crear el alias, como se muestra aquí, donde el parámetro con valores de tabla tiene el alias "EC":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

En este ejemplo de Transact-SQL se muestra cómo seleccionar las filas de un parámetro con valores de tabla para realizar una inserción en una sola operación basada en conjuntos.

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>Limitaciones de los parámetros con valores de tabla

Existen varias limitaciones para los parámetros con valores de tabla:  
  
- No se pueden pasar parámetros con valores de tabla a funciones definidas por el usuario.  
  
- Los parámetros con valores de tabla solo se pueden indizar para admitir restricciones UNIQUE o PRIMAry KEY. SQL Server no mantiene estadísticas en los parámetros con valores de tabla.  
  
- Los parámetros con valores de tabla son de solo lectura en código de Transact-SQL. No se pueden actualizar los valores de columna de las filas de un parámetro con valores de tabla y no se pueden insertar ni eliminar filas. Para modificar los datos que se pasan a un procedimiento almacenado o a una instrucción con parámetros en el parámetro con valores de tabla, debe insertar los datos en una tabla temporal o en una variable de tabla.  
  
- No se pueden usar instrucciones ALTER TABLE para modificar el diseño de parámetros con valores de tabla.

- Puede transmitir objetos grandes en un parámetro con valores de tabla.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configuración de un parámetro con valores de tabla

A partir de Microsoft JDBC driver 6,0 para SQL Server, se admiten parámetros con valores de tabla con una instrucción con parámetros o un procedimiento almacenado parametrizado. Los parámetros con valores de tabla se pueden rellenar a partir de un SQLServerDataTable, de un conjunto de resultados o de una implementación proporcionada por el usuario de la interfaz ISQLServerDataRecord. Al establecer un parámetro con valores de tabla para una consulta preparada, debe especificar un nombre de tipo que debe coincidir con el nombre de un tipo compatible creado previamente en el servidor.  
  
Los dos fragmentos de código siguientes muestran cómo configurar un parámetro con valores de tabla con SQLServerPreparedStatement y con SQLServerCallableStatement para insertar datos. Aquí sourceTVPObject puede ser SQLServerDataTable, o un conjunto de resultados o un objeto ISQLServerDataRecord. En los ejemplos se supone que la conexión es un objeto de conexión activo.  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
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
> Consulte **la sección API de parámetros con valores de tabla para el controlador JDBC** siguiente para obtener una lista completa de las API disponibles para establecer el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Pasar un parámetro con valores de tabla como un objeto SQLServerDataTable  

A partir de Microsoft JDBC driver 6,0 para SQL Server, la clase SQLServerDataTable representa una tabla en memoria de datos relacionales. En este ejemplo se muestra cómo construir un parámetro con valores de tabla a partir de datos en memoria mediante el objeto SQLServerDataTable. En primer lugar, el código crea un objeto SQLServerDataTable, define su esquema y rellena la tabla con datos. A continuación, el código configura un SQLServerPreparedStatement que pasa esta tabla de datos como un parámetro con valores de tabla a SQL Server.  

```java
/* Assumes connection is an active Connection object. */

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
> Consulte **la sección API de parámetros con valores de tabla para el controlador JDBC** siguiente para obtener una lista completa de las API disponibles para establecer el parámetro con valores de tabla.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Pasar un parámetro con valores de tabla como un objeto ResultSet  

En este ejemplo se muestra cómo transmitir por secuencias filas de datos de un conjunto de resultados a un parámetro con valores de tabla. El código recupera primero los datos de una tabla de origen en una crea un objeto SQLServerDataTable, define su esquema y rellena la tabla con datos. A continuación, el código configura un SQLServerPreparedStatement que pasa esta tabla de datos como un parámetro con valores de tabla a SQL Server.  

```java
/* Assumes connection is an active Connection object. */

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
> Consulte **la sección API de parámetros con valores de tabla para el controlador JDBC** siguiente para obtener una lista completa de las API disponibles para establecer el parámetro con valores de tabla.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Pasar un parámetro con valores de tabla como un objeto ISQLServerDataRecord  

A partir de Microsoft JDBC driver 6,0 para SQL Server, hay disponible una nueva interfaz ISQLServerDataRecord para los datos de streaming (en función de cómo el usuario proporcione la implementación) mediante un parámetro con valores de tabla. En el ejemplo siguiente se muestra cómo implementar la interfaz ISQLServerDataRecord y cómo pasarla como un parámetro con valores de tabla. Para simplificar, en el ejemplo siguiente se pasa una sola fila con valores codificados en el parámetro con valores de tabla. Idealmente, el usuario implementaría esta interfaz para transmitir filas desde cualquier origen, por ejemplo, de archivos de texto.  

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
> Consulte **la sección API de parámetros con valores de tabla para el controlador JDBC** siguiente para obtener una lista completa de las API disponibles para establecer el parámetro con valores de tabla.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>API de parámetros con valores de tabla para el controlador JDBC

### <a name="sqlservermetadata"></a>SQLServerMetaData

Esta clase representa los metadatos de una columna. Se utiliza en la interfaz ISQLServerDataRecord para pasar metadatos de columna al parámetro con valores de tabla. Los métodos de esta clase son:  

| Nombre                                                                                                                                                                             | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Public SQLServerMetaData (String columnName, int sqlType, int Precision, int Scale, Boolean useServerDefault, Boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna, el tipo SQL, la precisión, la escala y el valor predeterminado del servidor especificados. Esta forma del constructor admite parámetros con valores de tabla permitiéndole especificar si la columna es única en el parámetro con valores de tabla, el criterio de ordenación de la columna y el ordinal de la columna de ordenación. <br/><br/>useServerDefault: especifica si esta columna debe usar el valor de servidor predeterminado; El valor predeterminado es false.<br>isUniqueKey: indica si la columna del parámetro con valores de tabla es única; El valor predeterminado es false.<br>sortOrder: indica el criterio de ordenación de una columna; El valor predeterminado es SQLServerSortOrder. no especificado.<br>sortOrdinal: especifica el ordinal de la columna de ordenación; sortOrdinal comienza en 0; El valor predeterminado es-1. |
| Public SQLServerMetaData (String columnName, int sqlType)                                                                                                                        | Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna y el tipo SQL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Public SQLServerMetaData (String columnName, int sqlType, int length)                                                                                                                        | Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna, el tipo SQL y la longitud (para los datos de cadena). La longitud se usa para diferenciar cadenas grandes de cadenas con una longitud inferior a 4000 caracteres. Introducido en la versión 7,2 del controlador JDBC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Public SQLServerMetaData (String columnName, int sqlType, int Precision, int Scale)                                                                                              | Inicializa una nueva instancia de SQLServerMetaData con el nombre de columna, el tipo SQL, la precisión y la escala.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData (SQLServerMetaData sqlServerMetaData)                                                                                                                    | Inicializa una nueva instancia de SQLServerMetaData desde otro objeto SQLServerMetaData.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public string getColumName ()                                                                                                                                                     | Recupera el nombre de la columna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Recupera el tipo SQL de Java.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | Recupera la precisión del tipo pasado a la columna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale ()                                                                                                                                                            | Recupera la escala del tipo pasado a la columna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerSortOrder getSortOrder ()                                                                                                                                         | Recupera el criterio de ordenación.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal ()                                                                                                                                                      | Recupera el ordinal de ordenación.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Public Boolean isUniqueKey ()                                                                                                                                                     | Devuelve si la columna es única.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public Boolean useServerDefault ()                                                                                                                                                | Devuelve un valor que indica si la columna utiliza el valor de servidor predeterminado.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

Enumeración que define el criterio de ordenación. Los valores posibles son ascendente, descendente y sin especificar.
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

Esta clase representa una tabla de datos en memoria que se va a usar con parámetros con valores de tabla. Los métodos de esta clase son:  

| Nombre                                                          | Descripción                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | Inicializa una nueva instancia de SQLServerDataTable.    |
| el iterador público\<< entero de entrada, objeto [] > > getIterator ()      | Recupera un iterador en las filas de la tabla de datos. |
| public void addColumnMetadata (String columnName, int sqlType) | Agrega metadatos para la columna especificada.              |
| public void addColumnMetadata (columna SQLServerDataColumn)     | Agrega metadatos para la columna especificada.              |
| public void addRow (objeto... valor                          | Agrega una fila de datos a la tabla de datos.              |
| entero de\<mapa público, SQLServerDataColumn > getColumnMetadata () | Recupera los metadatos de la columna de esta tabla de datos.       |
| eliminación de void público ()                                           | Borra esta tabla de datos.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

Esta clase representa una columna de la tabla de datos en memoria representada por SQLServerDataTable. Los métodos de esta clase son:  

| Nombre                                                       | Descripción                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Public SQLServerDataColumn (String columnName, int sqlType) | Inicializa una nueva instancia de SQLServerDataColumn con el nombre y el tipo de columna. |
| public string getColumnName ()                              | Recupera el nombre de la columna.                                                       |
| public int getColumnType ()                                 | Recupera el tipo de columna.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

Esta clase representa una interfaz que los usuarios pueden implementar para transmitir los datos a un parámetro con valores de tabla. Los métodos de esta interfaz son:  
  
| Nombre                                                    | Descripción                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Public SQLServerMetaData getColumnMetaData (columna int); | Recupera los metadatos de columna del índice de columna especificado.                                               |
| public int getColumnCount ();                            | Recupera el número total de columnas.                                                                  |
| public Object[] getRowData();                           | Recupera los datos de la fila actual como una matriz de objetos.                                          |
| public boolean next();                                  | Se desplaza a la siguiente fila. Devuelve true si el movimiento se realiza correctamente y hay una fila siguiente; en caso contrario, false. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

Se han agregado los siguientes métodos a esta clase para admitir el paso de parámetros con valores de tabla.  

| Nombre                                                                                                    | Descripción                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public void setStructured (int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | Rellena un parámetro con valores de tabla con una tabla de datos. parameterIndex es el índice de parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpDataTable es el objeto de tabla de datos de origen.                                                                                                          |
| public void setStructured (int parameterIndex, String tvpName, ResultSet tvpResultSet)             | Rellena un parámetro con valores de tabla con un conjunto de resultados recuperado de otra tabla. parameterIndex es el índice del parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpResultSet es el objeto del conjunto de resultados de origen.                                                                               |
| public void setStructured (int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | Rellena un parámetro con valores de tabla con un objeto ISQLServerDataRecord. ISQLServerDataRecord se utiliza para transmitir datos por secuencias y el usuario decide cómo usarlo. parameterIndex es el índice del parámetro, tvpName es el nombre del parámetro con valores de tabla y tvpDataRecord es un objeto ISQLServerDataRecord. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

Se han agregado los siguientes métodos a esta clase para admitir el paso de parámetros con valores de tabla.  
  
| Nombre                                                                                                        | Descripción                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public void setStructured (String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con una tabla de datos. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpDataTable es el objeto de tabla de datos.                                                                                                                 |
| public void setStructured (String paratemeterName, String tvpName, ResultSet tvpResultSet)             | Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con un conjunto de resultados recuperado de otra tabla. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpResultSet es el objeto del conjunto de resultados de origen.                                                                              |
| public void setStructured (String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | Rellena un parámetro con valores de tabla que se pasa a un procedimiento almacenado con un objeto ISQLServerDataRecord. ISQLServerDataRecord se utiliza para transmitir datos por secuencias y el usuario decide cómo usarlo. paratemeterName es el nombre del parámetro, tvpName es el nombre del tipo TVP y tvpDataRecord es un objeto ISQLServerDataRecord. |

## <a name="see-also"></a>Consulte también

[Introducción al controlador JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
