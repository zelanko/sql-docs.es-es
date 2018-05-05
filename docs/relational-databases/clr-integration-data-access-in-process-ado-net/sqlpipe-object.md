---
title: SqlPipe, objetos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 15786a3af4b6598f73c822a8196039ec3e335d2a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlpipe-object"></a>SqlPipe, objetos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]es muy común escribir un procedimiento almacenado (o un procedimiento almacenado extendido) que envía resultados o parámetros de salida al cliente que realiza la llamada.  
  
 En un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] , cualquier instrucción **SELECT** que devuelve cero o más filas envía los resultados a la "canalización" del autor de la llamada conectado.  
  
 En los objetos de base de datos de Common Language Runtime (CLR) que se ejecutan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede enviar los resultados a la canalización conectada mediante los métodos **Send** del objeto **SqlPipe** . Para obtener el objeto **Pipe** , debe obtener acceso a la propiedad **SqlContext** del objeto **SqlPipe** . La clase **SqlPipe** es conceptualmente similar a la clase **Response** incluida en ASP.NET. Para obtener más información, vea la documentación de referencia de la clase SqlPipe en el kit de desarrollo de software de .NET Framework.  
  
## <a name="returning-tabular-results-and-messages"></a>Devolver mensajes y resultados tabulares  
 **SqlPipe** incluye un método **Send** , que cuenta con tres sobrecargas. Estas sobrecargas son:  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 El método **Send** envía los datos directamente al cliente o autor de la llamada. Generalmente es el cliente el que consume los resultados del método **SqlPipe**, pero en el caso de procedimientos almacenados de CLR anidados, el consumidor de los resultados también puede ser un procedimiento almacenado. Por ejemplo, Procedure1 llama a SqlCommand.ExecuteReader() con el texto de comando "EXEC Procedure2". Procedure2 también es un procedimiento almacenado administrado. Si Procedure2 llama ahora a SqlPipe.Send( SqlDataRecord ), la fila se envía al lector de Procedure1, no al cliente.  
  
 El **enviar** método envía un mensaje de cadena que aparece en el cliente como un mensaje informativo, equivalente a PRINT en [!INCLUDE[tsql](../../includes/tsql-md.md)]. También puede enviar un conjunto de resultados de fila única mediante **SqlDataRecord**o un conjunto de resultados de varias filas mediante **SqlDataReader**.  
  
 El objeto **SqlPipe** también incluye un método **ExecuteAndSend** . Este método se puede utilizar para ejecutar un comando (se pasa como objeto **SqlCommand** ) y devolver directamente los resultados al autor de la llamada. Si existen errores en el comando enviado, las excepciones se envían a la canalización, pero también se envía una copia al código administrado que realiza la llamada. Si el código de llamada no detecta la excepción, propaga la pila al código de [!INCLUDE[tsql](../../includes/tsql-md.md)] y aparece dos veces en el resultado. Si el código de llamada sí detecta la excepción, el consumidor de la canalización aún ve el error, pero no hay errores duplicados.  
  
 Puede tomar solamente un **SqlCommand** asociado a la conexión contextual; no puede tomar ningún comando asociado a la conexión no contextual.  
  
## <a name="returning-custom-result-sets"></a>Devolver conjuntos de resultados personalizados  
 Los procedimientos almacenados administrados pueden enviar conjuntos de resultados que no proceden de **SqlDataReader**. El método **SendResultsStart** , junto con **SendResultsRow** y **SendResultsEnd**, permite a los procedimientos almacenados enviar conjuntos de resultados personalizados al cliente.  
  
 **SendResultsStart** toma como entrada un **SqlDataRecord** . Este método marca el principio de un conjunto de resultados y utiliza los metadatos del registro para generar los metadatos que describen el conjunto de resultados. No envía el valor del registro con **SendResultsStart**. Todas las filas subsiguientes, enviadas mediante el método **SendResultsRow**, deben coincidir con la definición de los metadatos.  
  
> [!NOTE]  
>  Después de llamar al método **SendResultsStart** , solo se puede llamar a **SendResultsRow** y **SendResultsEnd** . La llamada a cualquier otro método en la misma instancia de **SqlPipe** produce una excepción **InvalidOperationException**. **SendResultsEnd** devuelve **SqlPipe** al estado inicial con el que se puede llamar a otros métodos.  
  
### <a name="example"></a>Ejemplo  
 El procedimiento almacenado **uspGetProductLine** devuelve el nombre, el número de producto, el color y el precio de todos los productos de una línea de productos especificada. Este procedimiento almacenado acepta coincidencias exactas de *prodLine*.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] ejecuta el procedimiento **uspGetProduct** , que devuelve una lista de productos de bicicleta de paseo.  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>Vea también  
 [SqlDataRecord, objeto](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [Procedimientos almacenados de CLR](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Extensiones específicas en proceso de SQL Server a ADO.NET](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
