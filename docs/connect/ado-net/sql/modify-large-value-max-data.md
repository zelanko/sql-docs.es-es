---
title: Modificación de datos de valores grandes (max) en ADO.NET
description: Describe cómo trabajar con tipos de datos de valores grandes.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: fac55eb25f89ced173683d5ed5d4334c2fcde975
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452124"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>Modificación de datos de valores grandes (max) en ADO.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Los tipos de datos de objeto grande (LOB) son aquellos que superan el tamaño máximo de fila de 8 kilobytes (KB). SQL Server proporciona un especificador `max` para los tipos de datos `varchar`, `nvarchar` y `varbinary` que permite el almacenamiento de valores tan grandes como 2^32 bytes. Las columnas de tabla y las variables de Transact-SQL pueden especificar tipos de datos `varchar(max)`, `nvarchar(max)` o `varbinary(max)`. En .NET, los tipos de datos `max` se pueden obtener mediante `DataReader`, y también se pueden especificar como valores de parámetro de entrada y salida sin ningún control especial. En el caso de los tipos de datos de gran `varchar`, los datos se pueden recuperar y actualizar incrementalmente.  
  
Los tipos de datos `max` se pueden usar para comparaciones, como variables de Transact-SQL y para la concatenación. También se pueden usar en las cláusulas DISTINCt, ORDER BY, GROUP BY de una instrucción SELECT, así como en agregados, combinaciones y subconsultas.

Vea [uso de tipos de datos de valores grandes](https://go.microsoft.com/fwlink/?LinkId=120498) en libros en pantalla de SQL Server más información sobre los tipos de datos de valores grandes.
  
## <a name="large-value-type-restrictions"></a>Restricciones de tipo de valor grande  
Las restricciones siguientes se aplican a los tipos de datos `max`, que no existen para tipos de datos más pequeños:  
  
- Un `sql_variant` no puede contener un tipo de datos de `varchar` grande.  
  
- No se pueden especificar columnas de `varchar` grande como columna de clave en un índice. Se permiten en una columna incluida en un índice no clúster.  
  
- Las columnas de `varchar` grande no se pueden usar como columnas de clave de partición.  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Trabajo con tipos de valor grande en Transact-SQL  
La función `OPENROWSET` de Transact-SQL es un método único de conexión y acceso a los datos remotos. Se puede hacer referencia a `OPENROWSET` en la cláusula FROM de una consulta como si fuera un nombre de tabla. También se puede hacer referencia como la tabla de destino de una instrucción INSERT, UPDATE o DELETE.  
  
La función `OPENROWSET` incluye el `BULK` proveedor de conjuntos de filas, que permite leer datos directamente desde un archivo sin cargar los datos en una tabla de destino. Esto permite usar `OPENROWSET` en una instrucción INSERT SELECT simple.  
  
Los argumentos de la opción `OPENROWSET BULK` ofrecen un control significativo sobre dónde comienza y termina la lectura de datos, cómo tratar los errores y cómo interpretar los datos. Por ejemplo, puede especificar que el archivo de datos se lea como un conjunto de filas de una sola fila y una sola columna de tipo `varbinary`, `varchar` o `nvarchar`. Para obtener la sintaxis y las opciones completas, vea Libros en pantalla de SQL Server.  
  
En el ejemplo siguiente se inserta una foto en la tabla ProductPhoto de la base de datos de ejemplo AdventureWorks. Si usa el proveedor `BULK OPENROWSET`, debe proporcionar la lista con nombre de columnas, incluso aunque no inserte valores en todas las columnas. En este caso, la clave principal se define como una columna de identidad y se puede omitir en la lista de columnas. Tenga en cuenta que también debe proporcionar un nombre de correlación al final de la instrucción `OPENROWSET`, que en este caso es ThumbnailPhoto. Esto se correlaciona con la columna de la tabla `ProductPhoto` en la que se carga el archivo.  
  
```sql
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>Actualización de datos mediante UPDATE.WRITE  
La instrucción UPDATE de Transact-SQL tiene una nueva sintaxis de escritura para modificar el contenido de `varchar(max)`, `nvarchar(max)` o `varbinary(max)` columnas. Esto le permite realizar actualizaciones parciales de los datos. ACTUALIZACIÓN. La sintaxis de WRITE se muestra aquí en forma abreviada:  
  
UPDATE  
  
{ *\<objeto>* }  
  
SET  
  
{ *column_name* = {. WRITE ( *expresión* , @Offset, @Length)}  
  
El método WRITE especifica que se va a modificar una sección del valor de *column_name*. La expresión es el valor que se va a copiar en *column_name*, mientras que `@Offset` es el punto inicial en el que se va a escribir la expresión y, por su parte, el argumento `@Length` es la longitud de la sección en la columna.  
  
|Si|Entonces|  
|--------|----------|  
|La expresión está establecida en NULL|`@Length` se omite y el valor de *column_name* se trunca en el elemento `@Offset` especificado.|  
|`@Offset` es NULL|La operación de actualización anexa la expresión al final del valor de *column_name* existente y se omite `@Length`.|  
|`@Offset` es mayor que la longitud del valor de column_name|SQL Server devuelve un error.|  
|`@Length` es NULL|La operación de actualización quita todos los datos de `@Offset` hasta el final del valor de `column_name`.|  
  
> [!NOTE]
>  Ni `@Offset` ni `@Length` pueden ser un número negativo.  
  
## <a name="example"></a>Ejemplo  
Este ejemplo de Transact-SQL actualiza un valor parcial en DocumentSummary, una columna `nvarchar(max)` de la tabla Document de la base de datos AdventureWorks. La palabra "components" se sustituye por la palabra "features" al especificar la palabra sustituta, la ubicación inicial (desplazamiento) de la palabra que se va a sustituir en los datos existentes y el número de caracteres que se va a sustituir (longitud). En el ejemplo se incluyen instrucciones SELECT antes y después de la instrucción UPDATE para comparar los resultados.  
  
```sql
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>Trabajo con tipos de valor grande en ADO.NET  
Puede trabajar con tipos de valor grande en ADO.NET si los especifica como objetos <xref:Microsoft.Data.SqlClient.SqlParameter> en <xref:Microsoft.Data.SqlClient.SqlDataReader> para que devuelvan un conjunto de resultados o mediante el uso de <xref:Microsoft.Data.SqlClient.SqlDataAdapter> para rellenar `DataSet`/`DataTable`. No hay ninguna diferencia entre la forma de trabajar con un tipo de valor grande y su tipo de datos de valor más pequeño relacionado.  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>Usar GetSqlBytes para recuperar datos  
El método `GetSqlBytes` del <xref:Microsoft.Data.SqlClient.SqlDataReader> se puede utilizar para recuperar el contenido de una columna `varbinary(max)`. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> denominado `cmd` que selecciona `varbinary(max)` datos de una tabla y un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos como <xref:System.Data.SqlTypes.SqlBytes>.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>Uso de GetSqlChars para recuperar datos  
El método `GetSqlChars` del <xref:Microsoft.Data.SqlClient.SqlDataReader> se puede utilizar para recuperar el contenido de una columna de `varchar(max)` o de `nvarchar(max)`. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> denominado `cmd` que selecciona `nvarchar(max)` datos de una tabla y un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos.   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>Usar GetSqlBinary para recuperar datos  
El método `GetSqlBinary` de una <xref:Microsoft.Data.SqlClient.SqlDataReader> se puede utilizar para recuperar el contenido de una columna `varbinary(max)`. El siguiente fragmento de código asume un objeto de <xref:Microsoft.Data.SqlClient.SqlCommand> denominado `cmd` que selecciona `varbinary(max)` datos de una tabla y un objeto de <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos como una secuencia de <xref:System.Data.SqlTypes.SqlBinary>.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>Usar GetBytes para recuperar datos  
El método `GetBytes` de una <xref:Microsoft.Data.SqlClient.SqlDataReader> Lee una secuencia de bytes del desplazamiento de columna especificado en una matriz de bytes a partir del desplazamiento de la matriz especificado. El siguiente fragmento de código asume un objeto de <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera bytes en una matriz de bytes. Tenga en cuenta que, a diferencia de `GetSqlBytes`, `GetBytes` requiere un tamaño para el búfer de la matriz.  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>Usar GetValue para recuperar datos  
El método `GetValue` de una <xref:Microsoft.Data.SqlClient.SqlDataReader> lee el valor del desplazamiento de columna especificado en una matriz. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos binarios del primer desplazamiento de columna y, a continuación, los datos de cadena del desplazamiento de la segunda columna.  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>Convertir tipos de valores grandes a tipos CLR  
Puede convertir el contenido de una `varchar(max)` o `nvarchar(max)` columna mediante cualquiera de los métodos de conversión de cadenas, como `ToString`. El siguiente fragmento de código asume un objeto de <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos.  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>Ejemplo  
El código siguiente recupera el nombre y el objeto `LargePhoto` de la tabla `ProductPhoto` de la base de datos `AdventureWorks` y los guarda en un archivo. El ensamblado debe compilarse con una referencia al espacio de nombres <xref:System.Drawing>.  El método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> del <xref:Microsoft.Data.SqlClient.SqlDataReader> devuelve un objeto <xref:System.Data.SqlTypes.SqlBytes> que expone una propiedad `Stream`. El código lo usa para crear un nuevo objeto `Bitmap` y, luego, lo guarda en el Gif `ImageFormat`.  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>Usar parámetros de tipo de valor grande  
Los tipos de valores grandes se pueden usar en objetos de <xref:Microsoft.Data.SqlClient.SqlParameter> de la misma manera que se usan los tipos de valor más pequeños en <xref:Microsoft.Data.SqlClient.SqlParameter> objetos. Puede recuperar tipos de valor grande como valores <xref:Microsoft.Data.SqlClient.SqlParameter>, como se muestra en el ejemplo siguiente. En el código se supone que existe el siguiente procedimiento almacenado GetDocumentSummary en la base de datos de ejemplo AdventureWorks. El procedimiento almacenado toma un parámetro de entrada denominado @DocumentID y devuelve el contenido de la columna DocumentSummary en el parámetro de salida @DocumentSummary.  
  
```sql
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>Ejemplo  
El código ADO.NET crea objetos <xref:Microsoft.Data.SqlClient.SqlConnection> y <xref:Microsoft.Data.SqlClient.SqlCommand> para ejecutar el procedimiento almacenado GetDocumentSummary y recuperar el resumen del documento, que se almacena como un tipo de valor grande. El código pasa un valor para el parámetro de entrada @DocumentID y muestra los resultados que se han vuelto a pasar en el parámetro de salida @DocumentSummary de la ventana Consola.  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>Pasos siguientes
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
- [Operaciones de datos de SQL Server en ADO.NET](sql-server-data-operations.md)
