---
title: Los desencadenadores CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- inserted tables
- database objects [CLR integration], triggers
- common language runtime [SQL Server], triggers
- updated columns
- building database objects [CLR integration], triggers
- triggers [CLR integration]
- deleted tables
- EventData property
- SqlTriggerContext class
- transactions [CLR integration]
ms.assetid: 302a4e4a-3172-42b6-9cc0-4a971ab49c1c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87d822e97a75bbd08375980fe6a6f0341d8f9c60
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158541"
---
# <a name="clr-triggers"></a>Desencadenadores CLR
  Debido a la integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR), es posible usar cualquier lenguaje [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para crear desencadenadores CLR. En esta sección se incluye información específica acerca de los desencadenadores implementados con la integración CLR. Para obtener una explicación completa de los desencadenadores, consulte [desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md).  
  
## <a name="what-are-triggers"></a>Qué son los desencadenadores  
 Un desencadenador es un tipo especial de procedimiento almacenado que se ejecuta automáticamente cuando se produce un evento de lenguaje. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye dos tipos de desencadenadores: desencadenadores del lenguaje de manipulación de datos (DML) y desencadenadores del lenguaje de definición de datos (DDL). Los desencadenadores DML pueden usarse cuando las instrucciones `INSERT`, `UPDATE` o `DELETE` modifican los datos de una tabla o vista especificada. Los desencadenadores DDL activan procedimientos almacenados en respuesta a una serie de instrucciones DDL, principalmente instrucciones que comienzan por `CREATE`, `ALTER` y `DROP`. Los desencadenadores DDL pueden usarse en tareas administrativas, como la auditoría y regulación de operaciones de base de datos.  
  
## <a name="unique-capabilities-of-clr-triggers"></a>Capacidades únicas de los desencadenadores CLR  
 Los desencadenadores escritos en [!INCLUDE[tsql](../../includes/tsql-md.md)] poseen la capacidad de determinar las columnas de la vista o de la tabla de activación que se han actualizado mediante el uso de las funciones `UPDATE(column)` y `COLUMNS_UPDATED()`.  
  
 Los desencadenadores escritos en lenguaje CLR se diferencian de otros objetos de integración CLR de varias formas significativas. Los desencadenadores CLR pueden:  
  
-   Hacer referencia a datos de las tablas `INSERTED` y `DELETED`  
  
-   Determinar las columnas que se han modificado como resultado de una operación `UPDATE`  
  
-   Obtener acceso a información acerca de los objetos de base de datos afectados por la ejecución de instrucciones DDL.  
  
 Estas capacidades se proporcionan de forma inherente en el lenguaje de consulta o por medio de la clase `SqlTriggerContext`. Para obtener información acerca de las ventajas de la integración de CLR y elegir entre código administrado y [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [información general de la integración CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="using-the-sqltriggercontext-class"></a>Usar la clase SqlTriggerContext  
 La clase `SqlTriggerContext` no puede construirse públicamente y solo puede obtenerse mediante el acceso a la propiedad `SqlContext.TriggerContext` dentro del cuerpo de un desencadenador CLR. La clase `SqlTriggerContext` puede obtenerse a partir del contexto `SqlContext` activo mediante una llamada a la propiedad `SqlContext.TriggerContext`:  
  
 `SqlTriggerContext myTriggerContext = SqlContext.TriggerContext;`  
  
 La clase `SqlTriggerContext` proporciona información de contexto acerca del desencadenador. Esta información contextual incluye el tipo de acción que provocó la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador DDL, una estructura XML `EventData` que describe la operación de desencadenamiento. Para obtener más información, consulte [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql).  
  
### <a name="determining-the-trigger-action"></a>Determinar la acción del desencadenador  
 Una vez que ha obtenido un `SqlTriggerContext`, puede usarlo para determinar el tipo de acción que provocó que se activara el desencadenador. Esta información se encuentra disponible a través de la propiedad `TriggerAction` de la clase `SqlTriggerContext`.  
  
 En el caso de los desencadenadores DML, la propiedad `TriggerAction` puede tener uno de los siguientes valores:  
  
-   TriggerAction.Update (0x1)  
  
-   TriggerAction.Insert (0x2)  
  
-   TriggerAction.Delete (0x3)  
  
-   En el caso de los desencadenadores DDL, la lista de valores posibles de TriggerAction es bastante más larga. Para obtener más información, vea el tema relativo a la enumeración TriggerAction en el SDK de .NET Framework.  
  
### <a name="using-the-inserted-and-deleted-tables"></a>Uso de las tablas insertadas y eliminadas  
 Se usan dos tablas especiales en las instrucciones de desencadenadores DML: el **insertado** tabla y el **eliminado** tabla. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea y administra automáticamente ambas tablas. Puede usar estas tablas temporales para probar los efectos de determinadas modificaciones en los datos y para establecer condiciones para las acciones de los desencadenadores DML; sin embargo, no es posible modificar los datos de las tablas directamente.  
  
 Los desencadenadores CLR pueden tener acceso a la **insertado** y **eliminado** tablas a través del proveedor en proceso CLR. Para ello, se obtiene un objeto `SqlCommand` del objeto SqlContext. Por ejemplo:  
  
 C#  
  
```  
SqlConnection connection = new SqlConnection ("context connection = true");  
connection.Open();  
SqlCommand command = connection.CreateCommand();  
command.CommandText = "SELECT * from " + "inserted";  
```  
  
 Visual Basic  
  
```  
Dim connection As New SqlConnection("context connection=true")  
Dim command As SqlCommand  
connection.Open()  
command = connection.CreateCommand()  
command.CommandText = "SELECT * FROM " + "inserted"  
```  
  
### <a name="determining-updated-columns"></a>Determinar las columnas actualizadas  
 Puede determinar el número de columnas que se han modificado en una operación UPDATE mediante el uso de la propiedad `ColumnCount` del objeto `SqlTriggerContext`. Puede usar el método `IsUpdatedColumn`, que toma el ordinal de la columna como parámetro de entrada, para determinar si la columna se ha actualizado. Un valor `True` indica que la columna se ha actualizado.  
  
 Por ejemplo, este fragmento de código (del desencadenador EmailAudit que se muestra más adelante en este tema) muestra todas las columnas actualizadas:  
  
 C#  
  
```  
reader = command.ExecuteReader();  
reader.Read();  
for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
{  
   pipe.Send("Updated column "  
      + reader.GetName(columnNumber) + "? "  
   + triggContext.IsUpdatedColumn(columnNumber).ToString());  
 }  
  
 reader.Close();  
```  
  
 Visual Basic  
  
```  
reader = command.ExecuteReader()  
reader.Read()  
Dim columnNumber As Integer  
  
For columnNumber=0 To triggContext.ColumnCount-1  
  
   pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
   "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
Next  
  
reader.Close()  
```  
  
### <a name="accessing-eventdata-for-clr-ddl-triggers"></a>Obtener acceso a EventData para desencadenadores DDL de CLR  
 Los desencadenadores DDL, al igual que los desencadenadores normales, activan procedimientos almacenados en respuesta a un evento. Pero, a diferencia de los desencadenadores DML, no se activan en respuesta a instrucciones UPDATE, INSERT o DELETE en una tabla o vista. En lugar de ello, se activan en respuesta a una serie de instrucciones DDL, principalmente instrucciones que comienzan por CREATE, ALTER y DROP. Los desencadenadores DDL pueden usarse en tareas administrativas, como la auditoría y supervisión de operaciones de base de datos y cambios de esquema.  
  
 Encontrará información acerca de un evento que activa un desencadenador DDL en la propiedad `EventData` de la clase `SqlTriggerContext`. Esta propiedad contiene un valor `xml`. El esquema XML incluye información acerca de:  
  
-   La hora del evento.  
  
-   El Id. de proceso del sistema (SPID) de la conexión durante la que se ha ejecutado el desencadenador.  
  
-   El tipo de evento que ha activado el desencadenador.  
  
 A continuación, en función del tipo de evento, el esquema incluirá información adicional, como la base de datos en la que se ha producido el evento, el objeto en el que se ha producido el evento y el comando [!INCLUDE[tsql](../../includes/tsql-md.md)] del evento.  
  
 En el ejemplo que se muestra a continuación, el siguiente desencadenador DDL devuelve la propiedad `EventData` sin formato.  
  
> [!NOTE]  
>  El envío de resultados y mensajes a través del objeto `SqlPipe` se muestra aquí únicamente como ejemplo y, en general, no se aconseja para el código de producción cuando se programan desencadenadores CLR. Otros datos devueltos pueden ser inesperados y conducir a errores en la aplicación.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   public static void DropTableTrigger()  
   {  
       SqlTriggerContext triggContext = SqlContext.TriggerContext;             
  
       switch(triggContext.TriggerAction)  
       {  
           case TriggerAction.DropTable:  
           SqlContext.Pipe.Send("Table dropped! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
  
           default:  
           SqlContext.Pipe.Send("Something happened! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
       }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    Public Shared Sub DropTableTrigger()  
        Dim triggContext As SqlTriggerContext  
        triggContext = SqlContext.TriggerContext  
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.DropTable  
              SqlContext.Pipe.Send("Table dropped! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
           Case Else  
              SqlContext.Pipe.Send("Something else happened! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
        End Select  
    End Sub  
End Class     
```  
  
 El siguiente resultado de ejemplo es el valor de la propiedad `EventData` tras la activación de un desencadenador DDL por parte de un evento `CREATE TABLE`  
  
 `<EVENT_INSTANCE><PostTime>2004-04-16T21:17:16.160</PostTime><SPID>58</SPID><EventType>CREATE_TABLE</EventType><ServerName>MACHINENAME</ServerName><LoginName>MYDOMAIN\myname</LoginName><UserName>MYDOMAIN\myname</UserName><DatabaseName>AdventureWorks</DatabaseName><SchemaName>dbo</SchemaName><ObjectName>UserName</ObjectName><ObjectType>TABLE</ObjectType><TSQLCommand><SetOptions ANSI_NULLS="ON" ANSI_NULL_DEFAULT="ON" ANSI_PADDING="ON" QUOTED_IDENTIFIER="ON" ENCRYPTED="FALSE" /><CommandText>create table dbo.UserName  
(  
 UserName varchar(50),  
 RealName varchar(50)  
)  
</CommandText></TSQLCommand></EVENT_INSTANCE>`  
  
 Además de la información accesible a través de la clase `SqlTriggerContext`, las consultas pueden seguir haciendo referencia a `COLUMNS_UPDATED` y inserted/deleted dentro del texto de un comando que se ejecuta en proceso.  
  
## <a name="sample-clr-trigger"></a>Desencadenador CLR de ejemplo  
 Para este ejemplo, considere un escenario donde se permita que el usuario elija el identificador que desee, pero usted desea saber qué usuarios en concreto han especificado una dirección de correo electrónico como identificador. El siguiente desencadenador detectará esa información y la registrará en una tabla de auditoría.  
  
> [!NOTE]  
>  El envío de resultados y mensajes a través del objeto `SqlPipe` se muestra aquí únicamente como ejemplo y, en general, no se aconseja para el código de producción. Otros datos devueltos pueden ser errores inesperados y conducir a aplicaciones  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   [SqlTrigger(Name = @"EmailAudit", Target = "[dbo].[Users]", Event = "FOR INSERT, UPDATE, DELETE")]  
   public static void EmailAudit()  
   {  
      string userName;  
      string realName;  
      SqlCommand command;  
      SqlTriggerContext triggContext = SqlContext.TriggerContext;  
      SqlPipe pipe = SqlContext.Pipe;  
      SqlDataReader reader;  
  
      switch (triggContext.TriggerAction)  
      {  
         case TriggerAction.Insert:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
            reader.Close();  
  
            if (IsValidEMailAddress(userName))  
            {  
               command = new SqlCommand(  
                  @"INSERT [dbo].[UserNameAudit] VALUES ('"  
                  + userName + @"', '" + realName + @"');",  
                  connection);  
               pipe.Send(command.CommandText);  
               command.ExecuteNonQuery();  
               pipe.Send("You inserted: " + userName);  
            }  
         }  
  
         break;  
  
         case TriggerAction.Update:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
  
            pipe.Send(@"You updated: '" + userName + @"' - '"  
               + realName + @"'");  
  
            for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
            {  
               pipe.Send("Updated column "  
                  + reader.GetName(columnNumber) + "? "  
                  + triggContext.IsUpdatedColumn(columnNumber).ToString());  
            }  
  
            reader.Close();  
         }  
  
         break;  
  
         case TriggerAction.Delete:  
            using (SqlConnection connection  
               = new SqlConnection(@"context connection=true"))  
               {  
                  connection.Open();  
                  command = new SqlCommand(@"SELECT * FROM DELETED;",  
                     connection);  
                  reader = command.ExecuteReader();  
  
                  if (reader.HasRows)  
                  {  
                     pipe.Send(@"You deleted the following rows:");  
                     while (reader.Read())  
                     {  
                        pipe.Send(@"'" + reader.GetString(0)  
                        + @"', '" + reader.GetString(1) + @"'");  
                     }  
  
                     reader.Close();  
  
                     //alternately, to just send a tabular resultset back:  
                     //pipe.ExecuteAndSend(command);  
                  }  
                  else  
                  {  
                     pipe.Send("No rows affected.");  
                  }  
               }  
  
               break;  
            }  
        }  
  
     public static bool IsValidEMailAddress(string email)  
     {  
         return Regex.IsMatch(email, @"^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$");  
     }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Text.RegularExpressions  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    <SqlTrigger(Name:="EmailAudit", Target:="[dbo].[Users]", Event:="FOR INSERT, UPDATE, DELETE")> _  
    Public Shared Sub EmailAudit()  
        Dim userName As String  
        Dim realName As String  
        Dim command As SqlCommand  
        Dim triggContext As SqlTriggerContext  
        Dim pipe As SqlPipe  
        Dim reader As SqlDataReader    
  
        triggContext = SqlContext.TriggerContext      
        pipe = SqlContext.Pipe    
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.Insert  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 reader.Close()  
  
                 If IsValidEmailAddress(userName) Then  
                     command = New SqlCommand("INSERT [dbo].[UserNameAudit] VALUES ('" & _  
                       userName & "', '" & realName & "');", connection)  
  
                    pipe.Send(command.CommandText)  
                    command.ExecuteNonQuery()  
                    pipe.Send("You inserted: " & userName)  
  
                 End If  
              End Using  
  
           Case TriggerAction.Update  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 pipe.Send("You updated: " & userName & " - " & realName)  
  
                 Dim columnNumber As Integer  
  
                 For columnNumber=0 To triggContext.ColumnCount-1  
  
                    pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
                      "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
                 Next  
  
                 reader.Close()  
              End Using  
  
           Case TriggerAction.Delete  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM DELETED;", connection)  
  
                 reader = command.ExecuteReader()  
  
                 If reader.HasRows Then  
                    pipe.Send("You deleted the following rows:")  
  
                    While reader.Read()  
  
                       pipe.Send( reader.GetString(0) & ", " & reader.GetString(1) )  
  
                    End While   
  
                    reader.Close()  
  
                    ' Alternately, just send a tabular resultset back:  
                    ' pipe.ExecuteAndSend(command)  
  
                 Else  
                   pipe.Send("No rows affected.")  
                 End If  
  
              End Using   
        End Select  
    End Sub  
  
    Public Shared Function IsValidEMailAddress(emailAddress As String) As Boolean  
  
       return Regex.IsMatch(emailAddress, "^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$")  
    End Function      
End Class  
```  
  
 Suponiendo que existen dos tablas con las siguientes definiciones:  
  
```  
CREATE TABLE Users  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
);  
GO CREATE TABLE UserNameAudit  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
)  
```  
  
 El [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción que crea el desencadenador en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es la siguiente y asume que el ensamblado **SQLCLRTest** ya está registrado en el actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  
  
```  
CREATE TRIGGER EmailAudit  
ON Users  
FOR INSERT, UPDATE, DELETE  
AS  
EXTERNAL NAME SQLCLRTest.CLRTriggers.EmailAudit  
```  
  
## <a name="validating-and-canceling-invalid-transactions"></a>Validar y cancelar las transacciones no válidas  
 Es normal usar desencadenadores para validar y cancelar transacciones INSERT, UPDATE o DELETE no válidas o para impedir que se realicen cambios en el esquema de la base de datos. Esto puede realizarse incorporando una lógica de validación en el desencadenador y, a continuación, revirtiendo la transacción actual si la acción no cumple los criterios de validación.  
  
 Cuando se llama al método `Transaction.Rollback` o a un objeto SqlCommand con el texto de comando "TRANSACTION ROLLBACK" dentro de un desencadenador, se inicia una excepción con un mensaje de error ambiguo y debe incluirse dentro de un bloque try/catch. El mensaje de error que aparece es similar al siguiente:  
  
```  
Msg 6549, Level 16, State 1, Procedure trig_InsertValidator, Line 0  
A .NET Framework error occurred during execution of user defined routine or aggregate 'trig_InsertValidator':   
System.Data.SqlClient.SqlException: Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting... User transaction, if any, will be rolled back.  
```  
  
 Se espera esta excepción y el bloque try/catch resulta necesario para que continúe la ejecución del código. Cuando finaliza la ejecución del código del desencadenador, se inicia otra excepción:  
  
```  
Msg 3991, Level 16, State 1, Procedure trig_InsertValidator, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate "trig_InsertValidator" has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting.  
The statement has been terminated.  
```  
  
 También se espera esta excepción y es necesario incluir un bloque try/catch alrededor de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que realiza la acción que activa el desencadenador para que la ejecución pueda continuar. A pesar de las dos excepciones iniciadas, la transacción se revierte y no se confirman los cambios en la tabla. Una diferencia importante entre los desencadenadores CLR y los desencadenadores [!INCLUDE[tsql](../../includes/tsql-md.md)] es que los desencadenadores [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden seguir realizando más trabajo una vez que se ha revertido la transacción.  
  
### <a name="example"></a>Ejemplo  
 El desencadenador siguiente realiza una validación simple de instrucciones INSERT en una tabla. Si el valor entero insertado es igual a uno, la transacción se revierte y el valor no se inserta en la tabla. El resto de los valores enteros se insertan en la tabla. Tenga en cuenta el bloque try/catch alrededor del método `Transaction.Rollback`. El script [!INCLUDE[tsql](../../includes/tsql-md.md)] crea una tabla de prueba, un ensamblado y un procedimiento almacenado administrado. Tenga en cuenta que las dos instrucciones INSERT se incluyen en un bloque try/catch, de modo que la excepción iniciada se detecta al finalizar la ejecución del desencadenador.  
  
 C#  
  
```  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class Triggers  
{  
    // Enter existing table or view for the target and uncomment the attribute line  
    // [Microsoft.SqlServer.Server.SqlTrigger (Name="trig_InsertValidator", Target="Table1", Event="FOR INSERT")]  
    public static void trig_InsertValidator()  
    {  
        using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
        {  
            SqlCommand command;  
            SqlDataReader reader;  
            int value;  
  
            // Open the connection.  
            connection.Open();  
  
            // Get the inserted value.  
            command = new SqlCommand(@"SELECT * FROM INSERTED", connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            value = (int)reader[0];  
            reader.Close();  
  
            // Rollback the transaction if a value of 1 was inserted.  
            if (1 == value)  
            {  
                try  
                {  
                    // Get the current transaction and roll it back.  
                    Transaction trans = Transaction.Current;  
                    trans.Rollback();                      
                }  
                catch (SqlException ex)  
                {  
                    // Catch the expected exception.                      
                }  
            }  
            else  
            {  
                // Perform other actions here.  
            }  
  
            // Close the connection.  
            connection.Close();              
        }  
    }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class Triggers  
' Enter existing table or view for the target and uncomment the attribute line  
' <Microsoft.SqlServer.Server.SqlTrigger(Name:="trig_InsertValidator", Target:="Table1", Event:="FOR INSERT")> _  
Public Shared Sub  trig_InsertValidator ()  
    Using connection As New SqlConnection("context connection=true")  
  
        Dim command As SqlCommand  
        Dim reader As SqlDataReader  
        Dim value As Integer  
  
        ' Open the connection.  
        connection.Open()  
  
        ' Get the inserted value.  
        command = New SqlCommand("SELECT * FROM INSERTED", connection)  
        reader = command.ExecuteReader()  
        reader.Read()  
        value = CType(reader(0), Integer)  
        reader.Close()  
  
        ' Rollback the transaction if a value of 1 was inserted.  
        If value = 1 Then  
  
            Try  
                ' Get the current transaction and roll it back.  
                Dim trans As Transaction  
                trans = Transaction.Current  
                trans.Rollback()  
  
            Catch ex As SqlException  
  
                ' Catch the exception.                      
            End Try  
        Else  
  
            ' Perform other actions here.  
        End If  
  
        ' Close the connection.  
        connection.Close()  
    End Using  
End Sub  
End Class  
```  
  
 Transact-SQL  
  
```  
-- Create the test table, assembly, and trigger.  
CREATE TABLE Table1(c1 int);  
go  
  
CREATE ASSEMBLY ValidationTriggers from 'E:\programming\ ValidationTriggers.dll';  
go  
  
CREATE TRIGGER trig_InsertValidator  
ON Table1  
FOR INSERT  
AS EXTERNAL NAME ValidationTriggers.Triggers.trig_InsertValidator;  
go  
  
-- Use a Try/Catch block to catch the expected exception  
BEGIN TRY  
   INSERT INTO Table1 VALUES(42)  
   INSERT INTO Table1 VALUES(1)  
END TRY  
BEGIN CATCH  
  SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
END CATCH;  
  
-- Clean up.  
DROP TRIGGER trig_InsertValidator;  
DROP ASSEMBLY ValidationTriggers;  
DROP TABLE Table1;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [Desencadenadores DML](../../relational-databases/triggers/dml-triggers.md)   
 [Desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [Creación de objetos de base de datos con Common Language Runtime &#40;CLR&#41; integración](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
