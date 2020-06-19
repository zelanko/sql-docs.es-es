---
title: Procedimientos almacenados CLR | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration], stored procedures
- stored procedures [CLR integration]
- common language runtime [SQL Server], stored procedures
- building database objects [CLR integration], stored procedures
- output parameters [CLR integration]
- tabular results
ms.assetid: bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4998058d55cd49c0eecfdecce2edc609a4d62c1f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933738"
---
# <a name="clr-stored-procedures"></a>Procedimientos almacenados de CLR
  Los procedimientos almacenados son rutinas que no pueden usarse en expresiones escalares. A diferencia de las funciones escalares, pueden devolver mensajes y resultados tabulares al cliente, invocar instrucciones del lenguaje de definición de datos (DDL) e instrucciones del lenguaje de manipulación de datos (DML), así como devolver parámetros de salida. Para obtener información sobre las ventajas de la integración CLR y la elección entre código administrado y [!INCLUDE[tsql](../../includes/tsql-md.md)] , consulte [información general sobre la integración CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-stored-procedures"></a>Requisitos de los procedimientos almacenados CLR  
 En el Common Language Runtime (CLR), los procedimientos almacenados se implementan como métodos estáticos públicos en una clase de un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ensamblado. El método estático puede declararse como void o devolver un valor entero. Si devuelve un valor entero, el entero devuelto se trata como el código de retorno del procedimiento. Por ejemplo:  
  
 `EXECUTE @return_status = procedure_name`  
  
 La @return_status variable contendrá el valor devuelto por el método. Si el método se declara como void, el código de retorno es 0.  
  
 Si el método toma parámetros, el número de parámetros de la implementación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] debe ser igual al número de parámetros utilizados en la declaración [!INCLUDE[tsql](../../includes/tsql-md.md)] del procedimiento almacenado.  
  
 Los parámetros pasados a un procedimiento almacenado CLR pueden ser cualquiera de los tipos nativos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tienen un equivalente en código administrado. Para crear el procedimiento mediante la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)], estos tipos deben especificarse con el tipo nativo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalente más adecuado. Para obtener más información sobre las conversiones de tipos, vea [asignar datos de parámetros CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
### <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 Los parámetros con valores de tabla (TVP), tipos de tabla definidos por el usuario que se pasan a un procedimiento o función, proporcionan un modo eficaz de pasar varias filas de datos al servidor. Los TVP presentan una funcionalidad similar a las matrices de parámetros, pero proporcionan más flexibilidad y una mayor integración con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También proporcionan la posibilidad de obtener mayor rendimiento. Además, los TVP ayudan a reducir el número de ciclos de ida y vuelta al servidor. En lugar de enviar varias solicitudes al servidor, como con una lista de parámetros escalares, los datos pueden enviarse al servidor como un TVP. Un tipo de tabla definido por el usuario no puede pasarse como un parámetro con valores de tabla a un procedimiento almacenado administrado o a una función que se ejecuta en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como tampoco puede devolverse desde dicho procedimiento o función. Para obtener más información sobre TVP, vea [usar parámetros con valores de tabla &#40;Motor de base de datos&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="returning-results-from-clr-stored-procedures"></a>Devolver resultados de los procedimientos almacenados CLR  
 La información puede devolverse de varios modos de los procedimientos almacenados de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], entre los que se incluyen parámetros de salida, resultados tabulares y mensajes.  
  
### <a name="output-parameters-and-clr-stored-procedures"></a>Parámetros OUTPUT y procedimientos almacenados CLR  
 Al igual que ocurre con los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)], puede devolverse información de los procedimientos almacenados de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] mediante el uso de parámetros OUTPUT. La sintaxis DML de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se utiliza para crear procedimientos almacenados de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] es igual que la que se utiliza para crear procedimientos almacenados escritos en [!INCLUDE[tsql](../../includes/tsql-md.md)]. El parámetro correspondiente en el código de implementación de la clase [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] debe usar un parámetro de paso por referencia como argumento. Tenga en cuenta que Visual Basic no admite parámetros de salida de la misma forma que en C#. Debe especificar el parámetro por referencia y aplicar el \<Out()> atributo para representar un parámetro de salida, como se muestra a continuación:  
  
```vb
Imports System.Runtime.InteropServices  
...  
Public Shared Sub PriceSum ( <Out()> ByRef value As SqlInt32)  
```  
  
 A continuación se muestra un procedimiento almacenado que devuelve información a través de un parámetro OUTPUT:  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void PriceSum(out SqlInt32 value)  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         value = 0;  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT Price FROM Products", connection);  
         SqlDataReader reader = command.ExecuteReader();  
  
         using (reader)  
         {  
            while( reader.Read() )  
            {  
               value += reader.GetSqlInt32(0);  
            }  
         }           
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Runtime.InteropServices  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Executes a query and iterates over the results to perform a summation.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
  
        Using connection As New SqlConnection("context connection=true")  
           value = 0  
           Connection.Open()  
           Dim command As New SqlCommand("SELECT Price FROM Products", connection)  
           Dim reader As SqlDataReader  
           reader = command.ExecuteReader()  
  
           Using reader  
              While reader.Read()  
                 value += reader.GetSqlInt32(0)  
              End While  
           End Using  
        End Using          
    End Sub  
End Class  
```  
  
 Cuando el ensamblado que contiene el procedimiento almacenado CLR anterior se ha compilado y creado en el servidor, [!INCLUDE[tsql](../../includes/tsql-md.md)] se utiliza lo siguiente para crear el procedimiento en la base de datos y se especifica *SUM* como parámetro de salida.  
  
```sql
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
-- if StoredProcedures class was inside a namespace, called MyNS,  
-- you would use:  
-- AS EXTERNAL NAME TestStoredProc.[MyNS.StoredProcedures].PriceSum  
```  
  
 Tenga en cuenta que *SUM* se declara como un `int` tipo de datos SQL Server y que el parámetro *Value* definido en el procedimiento almacenado CLR se especifica como un `SqlInt32` tipo de datos CLR. Cuando un programa que realiza la llamada ejecuta el procedimiento almacenado CLR, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte automáticamente el `SqlInt32` tipo de datos CLR a un `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.  Para obtener más información acerca de los tipos de datos CLR que se pueden y no se pueden convertir, vea [asignar datos de parámetros CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
### <a name="returning-tabular-results-and-messages"></a>Devolver mensajes y resultados tabulares  
 La devolución de mensajes y resultados tabulares al cliente se realiza a través del objeto `SqlPipe`, que se obtiene utilizando la propiedad `Pipe` de la clase `SqlContext`. El objeto `SqlPipe` tiene un método `Send`. Al llamar al método `Send`, puede transmitir datos a la aplicación que realiza la llamada a través de la canalización.  
  
 Existen varias sobrecargas del método `SqlPipe.Send`, incluida una que envía `SqlDataReader` y otra que simplemente envía una cadena de texto.  
  
###### <a name="returning-messages"></a>Devolver mensajes  
 Use `SqlPipe.Send(string)` para enviar mensajes a la aplicación cliente. El texto del mensaje está limitado a 8000 caracteres. Si el mensaje supera los 8000 caracteres, se truncará.  
  
###### <a name="returning-tabular-results"></a>Devolver resultados tabulares  
 Para enviar los resultados de una consulta directamente al cliente, use una de las sobrecargas del método `Execute` en el objeto `SqlPipe`. Se trata del modo más eficaz de devolver resultados al cliente, puesto que los datos se transfieren a los búferes de red sin copiarse en la memoria administrada. Por ejemplo:  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the results to the client directly.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void ExecuteToClient()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version", connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub ExecuteToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 Para enviar los resultados de una consulta previamente ejecutada a través del proveedor en proceso (o para preprocesar los datos mediante una implementación personalizada de `SqlDataReader`), use la sobrecarga del método `Send` que toma `SqlDataReader`. Este método es algo más lento que el método directo descrito anteriormente, pero ofrece mayor flexibilidad para manipular los datos antes de enviarlos al cliente.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the resulting reader to the client  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendReaderToClient()  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("select @@version", connection);  
         SqlDataReader r = command.ExecuteReader();  
         SqlContext.Pipe.Send(r);  
      }  
   }  
}  
```  
 
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendReaderToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class  
```  
  
 Para crear un conjunto de resultados dinámico, rellénelo y envíeselo al cliente; puede crear registros de la conexión actual y enviarlos mediante `SqlPipe.Send`.  
  
```csharp  
using System.Data;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
using System.Data.SqlTypes;  
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Create a result set on the fly and send it to the client.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendTransientResultSet()  
   {  
      // Create a record object that represents an individual row, including it's metadata.  
      SqlDataRecord record = new SqlDataRecord(new SqlMetaData("stringcol", SqlDbType.NVarChar, 128));  
  
      // Populate the record.  
      record.SetSqlString(0, "Hello World!");  
  
      // Send the record to the client.  
      SqlContext.Pipe.Send(record);  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendTransientResultSet()  
        ' Create a record object that represents an individual row, including it's metadata.  
        Dim record As New SqlDataRecord(New SqlMetaData("stringcol", SqlDbType.NVarChar, 128) )  
  
        ' Populate the record.  
        record.SetSqlString(0, "Hello World!")  
  
        ' Send the record to the client.  
        SqlContext.Pipe.Send(record)          
    End Sub  
End Class   
```  
  
 A continuación se muestra un ejemplo del envío de un mensaje y un resultado tabular a través de `SqlPipe`.  
  
```csharp  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void HelloWorld()  
   {  
      SqlContext.Pipe.Send("Hello world! It's now " + System.DateTime.Now.ToString()+"\n");  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT ProductNumber FROM ProductMaster", connection);  
         SqlDataReader reader = command.ExecuteReader();  
         SqlContext.Pipe.Send(reader);  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub HelloWorld()  
        SqlContext.Pipe.Send("Hello world! It's now " & System.DateTime.Now.ToString() & "\n")  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT ProductNumber FROM ProductMaster", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class   
```  
  
 El primer `Send` envía un mensaje al cliente, mientras que el segundo envía un resultado tabular mediante `SqlDataReader`.  
  
 Tenga en cuenta que se trata de ejemplos meramente ilustrativos. Las funciones CLR resultan más apropiadas que las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] simples para las aplicaciones que requieren un uso intensivo de los recursos para realizar cálculos. Un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] casi equivalente al ejemplo anterior es el siguiente:  
  
```sql
CREATE PROCEDURE HelloWorld() AS  
BEGIN  
PRINT('Hello world!')  
SELECT ProductNumber FROM ProductMaster  
END;  
```  
  
> [!NOTE]  
>  Los mensajes y los conjuntos de resultados se recuperan de manera diferente en la aplicación cliente. Por ejemplo, los [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conjuntos de resultados aparecen en la vista **resultados** y los mensajes aparecen en el panel **mensajes** .  
  
 Si el código de Visual C# anterior se guarda en un archivo MyFirstUdp.cs y se compila con:  
  
```console
csc /t:library /out:MyFirstUdp.dll MyFirstUdp.cs   
```  
  
 O bien, si el código de Visual Basic anterior se guarda en un archivo MyFirstUdp.vb y se compila con:  
  
```console
vbc /t:library /out:MyFirstUdp.dll MyFirstUdp.vb   
```  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], no se admiten la ejecución de objetos de base de datos de Visual C++ (como procedimientos almacenados) compilados con `/clr:pure`.  
  
 Es posible registrar el ensamblado resultante y el punto de entrada invocado con el siguiente DDL:  
  
```sql
CREATE ASSEMBLY MyFirstUdp FROM 'C:\Programming\MyFirstUdp.dll';  
CREATE PROCEDURE HelloWorld  
AS EXTERNAL NAME MyFirstUdp.StoredProcedures.HelloWorld;  
EXEC HelloWorld;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones definidas por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipos definidos por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Desencadenadores de CLR](../../../2014/database-engine/dev-guide/clr-triggers.md)  
  
  
