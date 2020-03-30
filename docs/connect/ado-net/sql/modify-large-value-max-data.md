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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9acbd8fb795fe1a14e77e5d746f729d37c11cc8d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896686"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>Modificación de datos de valores grandes (max) en ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Los tipos de datos de objeto grande (LOB) son aquellos que superan el tamaño máximo de fila de 8 kilobytes (KB). SQL Server proporciona un especificador `max` para los tipos de datos `varchar`, `nvarchar` y `varbinary` que permite el almacenamiento de valores tan grandes como 2^32 bytes. Las columnas de tabla y las variables de Transact-SQL pueden especificar tipos de datos `varchar(max)`, `nvarchar(max)` o `varbinary(max)`. En .NET, los tipos de datos `max` se pueden obtener mediante `DataReader`, y también se pueden especificar como valores de parámetro de entrada y salida sin ningún control especial. En el caso de los tipos de datos `varchar` grandes, los datos se pueden recuperar y actualizar incrementalmente.  
  
Los tipos de datos `max` se pueden usar para comparaciones, como variables de Transact-SQL y para la concatenación. También se pueden usar en las cláusulas DISTINCT, ORDER BY, GROUP BY de una instrucción SELECT, así como en agregados, combinaciones y subconsultas.

Vea [Usar tipos de datos de valores grandes](https://go.microsoft.com/fwlink/?LinkId=120498) en Libros en pantalla de SQL Server más detalles sobre los tipos de datos de valores grandes.
  
## <a name="large-value-type-restrictions"></a>Restricciones de tipo de valor grande  
Las restricciones siguientes se aplican a los tipos de datos `max`, que no existen para tipos de datos más pequeños:  
  
- Un `sql_variant` no puede contener un tipo de datos `varchar` grande.  
  
- No se pueden especificar columnas de `varchar` grandes como columna de clave en un índice. Se permiten en una columna incluida en un índice no agrupado.  
  
- Las columnas de `varchar` grandes no se pueden usar como columnas de clave de partición.  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Trabajo con tipos de valor grande en Transact-SQL  
La función `OPENROWSET` de Transact-SQL es un método único de conexión y acceso a los datos remotos. Se puede hacer referencia a `OPENROWSET` en la cláusula FROM de una consulta como si fuera un nombre de tabla. También se puede hacer referencia como la tabla de destino de una instrucción INSERT, UPDATE o DELETE.  
  
La función `OPENROWSET` incluye el proveedor de conjuntos de filas `BULK`, que permite leer los datos directamente de un archivo sin tener que cargarlos en una tabla de destino. Esto permite usar `OPENROWSET` en una instrucción INSERT SELECT simple.  
  
Los argumentos de la opción `OPENROWSET BULK` ofrecen un control significativo sobre dónde comienza y termina la lectura de datos, cómo tratar los errores y cómo interpretar los datos. Por ejemplo, puede especificar que el archivo de datos se lea como un conjunto de filas de una sola fila y una sola columna de tipo `varbinary`, `varchar` o `nvarchar`. Para obtener la sintaxis y las opciones completas, vea Libros en pantalla de SQL Server.  
  
En el ejemplo siguiente se inserta una foto en la tabla ProductPhoto de la base de datos de ejemplo de AdventureWorks. Si usa el proveedor `BULK OPENROWSET`, debe proporcionar la lista con nombre de columnas, incluso aunque no inserte valores en todas las columnas. En este caso, la clave principal se define como una columna de identidad y se puede omitir en la lista de columnas. Tenga en cuenta que también debe proporcionar un nombre de correlación al final de la instrucción `OPENROWSET`, que en este caso es ThumbnailPhoto. Esto se correlaciona con la columna de la tabla `ProductPhoto` en la que se carga el archivo.  
  
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
La instrucción UPDATE de Transact-SQL tiene una nueva sintaxis WRITE para modificar el contenido de las columnas `varchar(max)`, `nvarchar(max)` o `varbinary(max)`. Esto le permite realizar actualizaciones parciales de los datos. La sintaxis de UPDATE.WRITE se muestra aquí de forma abreviada:  
  
UPDATE  
  
{ *\<objeto>* }  
  
SET  
  
{ *column_name* = { .WRITE ( *expression* , @Offset , @Length ) }  
  
El método WRITE especifica que se va a modificar una sección del valor de *column_name*. La expresión es el valor que se va a copiar en *column_name*, mientras que `@Offset` es el punto inicial en el que se va a escribir la expresión y, por su parte, el argumento `@Length` es la longitud de la sección en la columna.  
  
|Si|Entonces|  
|--------|----------|  
|La expresión se configura en NULL.|`@Length` se omite y el valor de *column_name* se trunca en el elemento `@Offset` especificado.|  
|`@Offset` es NULL|La operación de actualización anexa la expresión al final del valor de *column_name* existente y se omite `@Length`.|  
|`@Offset` es mayor que la longitud del valor column_name.|SQL Server devuelve un error.|  
|`@Length` es NULL|La operación de actualización quita todos los datos de `@Offset` hasta el final del valor de `column_name`.|  
  
> [!NOTE]
>  `@Offset` ni `@Length` pueden ser un número negativo.  
  
## <a name="example"></a>Ejemplo  
En este ejemplo de Transact-SQL se actualiza un valor parcial en DocumentSummary, una columna `nvarchar(max)` de la tabla Document de la base de datos AdventureWorks. La palabra "components" se sustituye por la palabra "features" al especificar la palabra sustituta, la ubicación inicial (desplazamiento) de la palabra que se va a sustituir en los datos existentes y el número de caracteres que se va a sustituir (longitud). En el ejemplo se incluyen instrucciones SELECT antes y después de la instrucción UPDATE para comparar los resultados.  
  
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
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>Uso de GetSqlBytes para recuperar datos  
El método `GetSqlBytes` de <xref:Microsoft.Data.SqlClient.SqlDataReader> se puede utilizar para recuperar el contenido de una columna `varbinary(max)`. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> denominado `cmd` que selecciona datos `varbinary(max)` de una tabla y un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos como <xref:System.Data.SqlTypes.SqlBytes>.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>Uso de GetSqlChars para recuperar datos  
El método `GetSqlChars` de <xref:Microsoft.Data.SqlClient.SqlDataReader> se puede utilizar para recuperar el contenido de una columna `varchar(max)` o `nvarchar(max)`. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> denominado `cmd` que selecciona datos `nvarchar(max)` de una tabla y un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos.   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>Uso de GetSqlBinary para recuperar datos  
El método `GetSqlBinary` de <xref:Microsoft.Data.SqlClient.SqlDataReader> se puede utilizar para recuperar el contenido de una columna `varbinary(max)`. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> denominado `cmd` que selecciona datos `varbinary(max)` de una tabla y un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos como un flujo <xref:System.Data.SqlTypes.SqlBinary>.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>Uso de GetBytes para recuperar datos  
El método `GetBytes` de <xref:Microsoft.Data.SqlClient.SqlDataReader> lee un flujo de bytes a partir del desplazamiento de la columna especificada en una matriz de bytes, comenzando en el desplazamiento de la matriz especificado. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera bytes en una matriz de bytes. Tenga en cuenta que, a diferencia de `GetSqlBytes`, `GetBytes` requiere un tamaño para el búfer de la matriz.  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>Uso de GetValue para recuperar datos  
El método `GetValue` de <xref:Microsoft.Data.SqlClient.SqlDataReader> lee el valor del desplazamiento de columna especificado en una matriz. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos binarios del desplazamiento de la primera columna y, a continuación, los datos de cadena del desplazamiento de la segunda columna.  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>Conversión de tipos de valores grandes a tipos CLR  
Puede convertir el contenido de una columna `varchar(max)` o `nvarchar(max)` mediante cualquiera de los métodos de conversión de cadenas, como `ToString`. El siguiente fragmento de código asume un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> denominado `reader` que recupera los datos.  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>Ejemplo  
El código siguiente recupera el nombre y el objeto `LargePhoto` de la tabla `ProductPhoto` de la base de datos `AdventureWorks` y los guarda en un archivo. El ensamblado debe compilarse con una referencia al espacio de nombres <xref:System.Drawing>.  El método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> de <xref:Microsoft.Data.SqlClient.SqlDataReader> devuelve un objeto <xref:System.Data.SqlTypes.SqlBytes> que expone una propiedad `Stream`. El código lo usa para crear un nuevo objeto `Bitmap` y, luego, lo guarda en el Gif `ImageFormat`.  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>Uso de parámetros de tipos de valores grandes  
Los tipos de valores grandes se pueden usar en objetos <xref:Microsoft.Data.SqlClient.SqlParameter> de la misma manera en que se usan los tipos de valores más pequeños en objetos <xref:Microsoft.Data.SqlClient.SqlParameter>. Puede recuperar tipos de valor grande como valores <xref:Microsoft.Data.SqlClient.SqlParameter>, como se muestra en el ejemplo siguiente. En el código se supone que existe el siguiente procedimiento almacenado GetDocumentSummary en la base de datos de ejemplo AdventureWorks. El procedimiento almacenado toma un parámetro de entrada denominado @DocumentID y devuelve el contenido de la columna DocumentSummary en el parámetro de salida @DocumentSummary.  
  
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
El código ADO.NET crea objetos <xref:Microsoft.Data.SqlClient.SqlConnection> y <xref:Microsoft.Data.SqlClient.SqlCommand> para ejecutar el procedimiento almacenado GetDocumentSummary y recuperar el resumen del documento, que se almacena como un tipo de valores grandes. El código pasa un valor para el parámetro de entrada @DocumentID y muestra los resultados que se han vuelto a pasar en el parámetro de salida @DocumentSummary de la ventana Consola.  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>Pasos siguientes
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
- [Operaciones de datos de SQL Server en ADO.NET](sql-server-data-operations.md)
