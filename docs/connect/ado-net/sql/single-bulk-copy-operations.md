---
title: Operaciones de copia masiva únicas.
description: Describe cómo realizar una única copia masiva de datos en una instancia de SQL Server mediante la clase SqlBulkCopy y cómo realizar la operación de copia masiva mediante instrucciones Transact-SQL y la clase SqlCommand.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 85d24b6695dfe9f592bfefabb13c2042cf3450c3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251171"
---
# <a name="single-bulk-copy-operations"></a>Operaciones de copia masiva únicas.

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

El método más sencillo para realizar una operación de copia masiva de SQL Server es realizar una operación única con una base de datos. De forma predeterminada, una operación de copia masiva se realiza como una operación aislada: la operación de copia tiene lugar sin transacciones y no es posible revertirla.  
  
> [!NOTE]
>  Si necesita revertir toda o parte de la copia masiva cuando se produce un error, puede usar una transacción administrada por <xref:Microsoft.Data.SqlClient.SqlBulkCopy> o realizar la operación de copia masiva en una transacción existente. **SqlBulkCopy** también funciona con <xref:System.Transactions> si la conexión está inscrita (implícita o explícitamente) en una transacción **System.Transactions**.  
>   
>  Para obtener más información, vea [Operaciones de transacción y de copia masiva](transaction-bulk-copy-operations.md).  
  
Los pasos generales para realizar una operación de copia masiva son los siguientes:  
  
1. Conéctese al servidor de origen y obtenga los datos que se van a copiar. Los datos también pueden provenir de otros orígenes, si se pueden recuperar de un objeto <xref:System.Data.IDataReader> o <xref:System.Data.DataTable>.  
  
2. Conéctese al servidor de destino (a menos que quiera que **SqlBulkCopy** establezca una conexión automáticamente).  
  
3. Cree un objeto de <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, estableciendo las propiedades necesarias.  
  
4. Establezca la propiedad **DestinationTableName** para indicar la tabla de destino de la operación de inserción masiva.  
  
5. Llame a uno de los métodos **WriteToServer**.  
  
6. Como opción, actualice las propiedades y llame de nuevo a **WriteToServer** si fuese necesario.  
  
7. Llame a <xref:Microsoft.Data.SqlClient.SqlBulkCopy.Close%2A>o ajuste las operaciones de copia masiva dentro de una instrucción `Using`.  
  
> [!CAUTION]
>  Se recomienda que los tipos de datos de la columna de origen y de destino coincidan. Si los tipos de datos no coinciden, **SqlBulkCopy** intenta convertir los valores de origen en el tipo de datos de destino mediante las reglas empleadas por <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>. Las conversiones pueden afectar al rendimiento y también pueden producir errores inesperados. Por ejemplo, un tipo de datos `Double` puede convertirse en un tipo de datos `Decimal` la mayoría de las veces, pero no siempre.  
  
## <a name="example"></a>Ejemplo  
La aplicación de consola siguiente muestra cómo cargar datos mediante la clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. En este ejemplo se usa <xref:Microsoft.Data.SqlClient.SqlDataReader> para copiar datos de la tabla **Production.Product** de la base de datos **AdventureWorks** de SQL Server en una tabla similar de la misma base de datos.  
  
> [!IMPORTANT]
>  Este ejemplo no se ejecuta a menos que haya creado las tablas de trabajo como se describe en [Configuración de ejemplos de copia masiva](bulk-copy-example-setup.md). Este código se proporciona para mostrar la sintaxis para usar **SqlBulkCopy**. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción `INSERT … SELECT` de Transact-SQL para copiar los datos.  
  
[!code-csharp[DataWorks SqlBulkCopy_WriteToServer#1](~/../sqlclient/doc/samples/SqlBulkCopy_WriteToServer.cs#1)]
  
## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>Realización de una operación de copia masiva mediante Transact-SQL y la clase Command  
En el ejemplo siguiente se muestra cómo usar el método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> para ejecutar la instrucción BULK INSERT.  
  
> [!NOTE]
>  La ruta de acceso al origen de datos depende del servidor. El proceso del servidor debe tener acceso a esa ruta para que la operación de copia masiva se realice correctamente.  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Operaciones de copia masiva en SQL Server](bulk-copy-operations-sql-server.md)
