---
title: Parámetros con valores de tabla
description: Describe cómo trabajar con parámetros con valores de tabla, que se introdujeron en SQL Server 2008.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: cb8eec87d0d36eb7deb8663e40407c0067967def
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451921"
---
# <a name="table-valued-parameters"></a>Parámetros con valores de tabla

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Los parámetros con valores de tabla proporcionan una manera sencilla de serializar varias filas de datos de una aplicación cliente en SQL Server sin necesidad de ir y volver repetidas veces ni de ninguna lógica especial de servidor para procesar los datos. Puede usar parámetros con valores de tabla para encapsular filas de datos en una aplicación cliente y enviar los datos al servidor en un único comando con parámetros. Las filas de datos entrantes se almacenan en una variable de tabla en la que, a continuación, se puede operar mediante el uso de Transact-SQL.  
  
El acceso a los valores de columna de los parámetros con valores de tabla se realiza con instrucciones estándar SELECT de Transact-SQL. Los parámetros con valores de tabla están fuertemente tipados y su estructura se valida automáticamente. El tamaño de los parámetros con valores de tabla solo está limitado por la memoria del servidor.  
  
> [!NOTE]
>  No se pueden devolver datos en un parámetro con valores de tabla. Los parámetros con valores de tabla son de solo entrada; no se admite la palabra clave OUTPUT.  
  
Para obtener más información sobre los parámetros con valores de tabla, vea los siguientes recursos.  
  
|Recurso|Descripción|  
|--------------|-----------------|  
|[Parámetros con valores de tabla (motor de base de datos)](https://go.microsoft.com/fwlink/?LinkId=98363) en los Libros en pantalla de SQL Server|Describe cómo crear y usar parámetros con valores de tabla.|  
|[Tipos de tabla definidos por el usuario](https://go.microsoft.com/fwlink/?LinkId=98364) en libros en pantalla de SQL Server|Describe los tipos de tabla definidos por el usuario que se usan para declarar parámetros con valores de tabla.|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Pasar varias filas en versiones anteriores de SQL Server  
Antes de la incorporación de los parámetros con valores de tabla a SQL Server 2008, las opciones para pasar varias filas de datos a un procedimiento almacenado o a un comando SQL con parámetros eran limitadas. Un desarrollador podría elegir entre las siguientes opciones para pasar varias filas al servidor:  
  
- Use una serie de parámetros individuales para representar los valores de varias columnas y filas de datos. La cantidad de datos que se pueden pasar mediante este método está limitada por el número de parámetros permitidos. Los procedimientos de SQL Server pueden tener 2100 parámetros como máximo. La lógica del lado servidor es necesaria para ensamblar estos valores individuales en una variable de tabla o una tabla temporal para su procesamiento.  
  
- Agrupar varios valores de datos en cadenas delimitadas o documentos XML y, a continuación, pasar esos valores de texto a un procedimiento o instrucción. Esto requiere que el procedimiento o la instrucción incluyan la lógica necesaria para validar las estructuras de datos y desagrupar los valores.  
  
- Cree una serie de instrucciones SQL individuales para las modificaciones de datos que afecten a varias filas, como las creadas llamando al método `Update` de una <xref:Microsoft.Data.SqlClient.SqlDataAdapter>. Los cambios se pueden enviar al servidor individualmente o por lotes en grupos. Sin embargo, incluso cuando se envían en lotes que contienen varias instrucciones, cada instrucción se ejecuta por separado en el servidor.  
  
- Utilice el programa de utilidad de `bcp` o el objeto <xref:Microsoft.Data.SqlClient.SqlBulkCopy> para cargar muchas filas de datos en una tabla. Aunque esta técnica es muy eficaz, no admite el procesamiento del lado servidor a menos que los datos se carguen en una tabla temporal o una variable de tabla.  
  
## <a name="creating-table-valued-parameter-types"></a>Crear tipos de parámetro con valores de tabla  
Los parámetros con valores de tabla se basan en estructuras de tabla fuertemente tipadas definidas mediante instrucciones CREATE TYPE de Transact-SQL. Debe crear un tipo de tabla y definir la estructura en SQL Server para poder usar los parámetros con valores de tabla en las aplicaciones de cliente. Para obtener más información sobre la creación de tipos de tabla, vea [Tipos de tabla definidos por el usuario](https://go.microsoft.com/fwlink/?LinkID=98364) en los Libros en pantalla de SQL Server.  
  
La instrucción siguiente crea un tipo de tabla denominado CategoryTableType que consta de las columnas CategoryID y CategoryName:  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
Después de crear un tipo de tabla, puede declarar parámetros con valores de tabla basados en ese tipo. El siguiente fragmento de Transact-SQL muestra cómo declarar un parámetro con valores de tabla en una definición de procedimiento almacenado. Tenga en cuenta que la palabra clave READONLY es necesaria para declarar un parámetro con valores de tabla.  
  
```sql
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modificar datos con parámetros con valores de tabla (Transact-SQL)  
Los parámetros con valores de tabla se pueden utilizar en las modificaciones de datos basadas en conjuntos que afectan a varias filas mediante la ejecución de una única instrucción. Por ejemplo, puede seleccionar todas las filas de un parámetro con valores de tabla e insertarlas en una tabla de base de datos, o puede crear una instrucción UPDATE combinando un parámetro con valores de tabla en la tabla que desea actualizar.  
  
La siguiente instrucción UPDATE de Transact-SQL muestra cómo usar un parámetro con valores de tabla al unirlo a la tabla Categories. Cuando se usa un parámetro con valores de tabla con una combinación en una cláusula FROM, también se debe crear el alias, como se muestra aquí, donde el parámetro con valores de tabla tiene el alias "EC":  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
Este ejemplo de Transact-SQL muestra cómo seleccionar filas de un parámetro con valores de tabla para ejecutar INSERT en una sola operación basada en conjuntos.  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>Limitaciones de los parámetros con valores de tabla  
Existen varias limitaciones para los parámetros con valores de tabla:  
  
- No puede pasar parámetros con valores de tabla a [funciones definidas por el usuario CLR](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md).  
  
- Los parámetros con valores de tabla solo se pueden indizar para admitir restricciones UNIQUE o PRIMAry KEY. SQL Server no mantiene estadísticas en los parámetros con valores de tabla.  
  
- Los parámetros con valores de tabla son de solo lectura en el código de Transact-SQL. No se pueden actualizar los valores de columna de las filas de un parámetro con valores de tabla y no se pueden insertar ni eliminar filas. Para modificar los datos que se pasan a un procedimiento almacenado o a una instrucción con parámetros en el parámetro con valores de tabla, debe insertar los datos en una tabla temporal o en una variable de tabla.  
  
- No se pueden usar instrucciones ALTER TABLE para modificar el diseño de parámetros con valores de tabla.  
  
## <a name="configuring-a-sqlparameter-example"></a>Configuración de un ejemplo de SqlParameter  
<xref:Microsoft.Data.SqlClient> permite rellenar parámetros con valores de tabla a partir de objetos <xref:System.Data.DataTable>, <xref:System.Data.Common.DbDataReader> o <xref:System.Collections.Generic.IEnumerable%601> \ <xref:Microsoft.Data.SqlClient.Server.SqlDataRecord>. Debe especificar un nombre de tipo para el parámetro con valores de tabla mediante la propiedad <xref:Microsoft.Data.SqlClient.SqlParameter.TypeName%2A> de <xref:Microsoft.Data.SqlClient.SqlParameter>. El `TypeName` debe coincidir con el nombre de un tipo compatible creado previamente en el servidor. En el fragmento de código siguiente se muestra cómo configurar <xref:Microsoft.Data.SqlClient.SqlParameter> para insertar datos.  
 
En el siguiente ejemplo, la variable `addedCategories` contiene <xref:System.Data.DataTable>. Para ver cómo se rellena la variable, vea los ejemplos de la sección siguiente, [pasar un parámetro con valores de tabla a un procedimiento almacenado](#passing).

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```   
  
También puede usar cualquier objeto derivado de <xref:System.Data.Common.DbDataReader> para transmitir filas de datos a un parámetro con valores de tabla, como se muestra en este fragmento:  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
## <a name="passing"></a> Paso de un parámetro con valores de tabla a un procedimiento almacenado  
En este ejemplo se muestra cómo pasar datos de parámetros con valores de tabla a un procedimiento almacenado. El código extrae las filas agregadas a una nueva <xref:System.Data.DataTable> mediante el método <xref:System.Data.DataTable.GetChanges%2A>. A continuación, el código define un <xref:Microsoft.Data.SqlClient.SqlCommand>, estableciendo la propiedad <xref:Microsoft.Data.SqlClient.SqlCommand.CommandType%2A> en <xref:System.Data.CommandType.StoredProcedure>. El <xref:Microsoft.Data.SqlClient.SqlParameter> se rellena con el método <xref:Microsoft.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> y el <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> se establece en `Structured`. A continuación, se ejecuta el <xref:Microsoft.Data.SqlClient.SqlCommand> mediante el método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>.  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>Pasar un parámetro con valores de tabla a una instrucción SQL con parámetros  
 En el ejemplo siguiente se muestra cómo insertar datos en DBO. Tabla Categories mediante una instrucción INSERT con una subconsulta SELECT que tiene un parámetro con valores de tabla como origen de datos. Al pasar un parámetro con valores de tabla a una instrucción SQL con parámetros, debe especificar un nombre de tipo para el parámetro con valores de tabla utilizando la nueva propiedad <xref:Microsoft.Data.SqlClient.SqlParameter.TypeName%2A> de una <xref:Microsoft.Data.SqlClient.SqlParameter>. Esta `TypeName` debe coincidir con el nombre de un tipo compatible creado previamente en el servidor. El código de este ejemplo usa la propiedad `TypeName` para hacer referencia a la estructura de tipo definida en DBO. CategoryTableType.  
  
> [!NOTE]
>  Si proporciona un valor para una columna de identidad en un parámetro con valores de tabla, debe emitir la instrucción SET IDENTITY_INSERT para la sesión.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =   
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>Streaming de filas con un DataReader  
También puede usar cualquier objeto derivado de <xref:System.Data.Common.DbDataReader> para transmitir filas de datos a un parámetro con valores de tabla. En el fragmento de código siguiente se muestra cómo recuperar datos de una base de datos de Oracle mediante un <xref:System.Data.OracleClient.OracleCommand> y un <xref:System.Data.OracleClient.OracleDataReader>. A continuación, el código configura un <xref:Microsoft.Data.SqlClient.SqlCommand> para invocar un procedimiento almacenado con un único parámetro de entrada. La propiedad <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> del <xref:Microsoft.Data.SqlClient.SqlParameter> está establecida en `Structured`. El <xref:Microsoft.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> pasa el conjunto de resultados `OracleDataReader` al procedimiento almacenado como un parámetro con valores de tabla.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Operaciones de datos de SQL Server en ADO.NET](sql-server-data-operations.md)
