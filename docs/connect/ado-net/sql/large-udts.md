---
title: UDT grandes
description: Muestra cómo recuperar datos de UDT de valor grande introducidos en SQL Server 2008.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4ea2c0002ceb01606cdf51f04246abcdc74429e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452151"
---
# <a name="large-udts"></a>UDT grandes

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Los tipos definidos por el usuario (UDT) permiten a los desarrolladores extender el sistema de tipo escalar del servidor mediante el almacenamiento de objetos de Common Language Runtime (CLR) en una base de datos de SQL Server. Los UDT pueden contener varios elementos y tener comportamientos, a diferencia de los tipos de datos de alias tradicionales, que se componen de un solo tipo de datos de sistema de SQL Server.  
  
Anteriormente, los UDT estaban restringidos a un tamaño máximo de 8 kilobytes. En SQL Server 2008, esta restricción se ha eliminado en los UDT con un formato de <xref:Microsoft.Data.SqlClient.Server.Format.UserDefined>.  
  
Para obtener la documentación completa de los tipos definidos por el usuario, consulte [tipos definidos por el usuario CLR](https://go.microsoft.com/fwlink/?LinkId=98366) en libros en pantalla de SQL Server.
  
## <a name="retrieving-udt-schemas-using-getschema"></a>Recuperar esquemas UDT mediante GetSchema  
El método <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> de <xref:Microsoft.Data.SqlClient.SqlConnection> devuelve información del esquema de la base de datos en un <xref:System.Data.DataTable>.
  
### <a name="getschematable-column-values-for-udts"></a>Valores de las columnas GetSchemaTable para UDT  
El método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> de una <xref:Microsoft.Data.SqlClient.SqlDataReader> devuelve un <xref:System.Data.DataTable> que describe los metadatos de la columna. En la tabla siguiente se describen las diferencias en los metadatos de columna para los UDT grandes entre SQL Server 2005 y SQL Server 2008.  
  
|Columna SqlDataReader|Resultado de|SQL Server 2008 y posterior|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|Varía|Varía|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|Instancia UDT|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|Instancia UDT|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|Nombre de tres partes especificado como *Database.SchemaName.TypeName*.|  
|`IsLong`|Varía|Varía|  
  
## <a name="sqldatareader-considerations"></a>Consideraciones de SqlDataReader  
<xref:Microsoft.Data.SqlClient.SqlDataReader> se ha ampliado a partir de SQL Server 2008 para admitir la recuperación de valores UDT grandes. La forma en que se procesan los valores UDT grandes mediante una <xref:Microsoft.Data.SqlClient.SqlDataReader> depende de la versión de SQL Server que esté utilizando, así como del `Type System Version` especificado en la cadena de conexión. Para obtener más información, vea <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
Los siguientes métodos de <xref:Microsoft.Data.SqlClient.SqlDataReader> devolverán una <xref:System.Data.SqlTypes.SqlBinary> en lugar de un UDT cuando el `Type System Version` se establezca en SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
Los métodos siguientes devolverán una matriz de `Byte[]` en lugar de un UDT cuando la `Type System Version` esté establecida en SQL Server 2005:  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
Tenga en cuenta que no se realiza ninguna conversión para la versión actual de ADO.NET.  
  
## <a name="specifying-sqlparameters"></a>Especificar SqlParameters  
Las siguientes propiedades de <xref:Microsoft.Data.SqlClient.SqlParameter> se han ampliado para trabajar con UDT grandes.  
  
|SqlParameter (propiedad)|Descripción|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Obtiene o establece un objeto que representa el valor del parámetro. El valor predeterminado es null. La propiedad puede ser `SqlBinary`, `Byte[]` o un objeto administrado.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Obtiene o establece un objeto que representa el valor del parámetro. El valor predeterminado es null. La propiedad puede ser `SqlBinary`, `Byte[]` o un objeto administrado.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Obtiene o establece el tamaño del valor del parámetro que se va a resolver. El valor predeterminado es 0. La propiedad puede ser un entero que represente el tamaño del valor del parámetro. En UDT grandes, puede ser el tamaño real del UDT o -1 si no se conoce.|  
  
## <a name="retrieving-data-example"></a>Ejemplo de recuperación de datos  
En el fragmento de código siguiente se muestra cómo recuperar datos UDT grandes. La variable `connectionString` supone una conexión válida a una base de datos de SQL Server y la variable `commandString` supone una instrucción SELECT válida con la columna de clave principal que aparece en primer lugar.  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
