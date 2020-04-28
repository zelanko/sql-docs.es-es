---
title: Funciones con valores de tabla de CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7dfd3db3a8193e92f9670213c602d55dc45f5c7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75232289"
---
# <a name="clr-table-valued-functions"></a>Funciones con valores de tabla en CLR
  Una función con valores de tabla es una función definida por el usuario que devuelve una tabla.  
  
 A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] amplía la funcionalidad de las funciones con valores de tabla ya que permite definir una función con valores de tabla en cualquier lenguaje administrado. Los datos de una función con valores de tabla se devuelven a través de un objeto `IEnumerable` o `IEnumerator`.  
  
> [!NOTE]  
>  En las funciones con valores de tabla, las columnas del tipo de tabla que devuelto no pueden incluir columnas de marca de tiempo ni columnas de tipo de datos de cadena no Unicode (como `char`, `varchar` y `text`). La restricción NOT NULL no se admite.  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Diferencias entre las funciones con valores de tabla de Transact-SQL y de CLR  
 Las funciones con valores de tabla de [!INCLUDE[tsql](../../includes/tsql-md.md)] materializan los resultados de la llamada a la función en una tabla intermedia. Puesto que utilizan una tabla intermedia, pueden admitir restricciones e índices únicos en los resultados. Estas características pueden resultar sumamente útiles cuando se devuelven resultados grandes.  
  
 Las funciones con valores de tabla en CLR, en cambio, representan una alternativa de transmisión por secuencias. No hay ningún requisito que obligue a materializar el conjunto de resultados en una única tabla. El plan de ejecución de la consulta que llama a la función con valores de tabla llama directamente al objeto `IEnumerable` devuelto por la función administrada y los resultados se consumen de manera incremental. Este modelo de transmisión por secuencias se asegura de que los resultados puedan consumirse inmediatamente después de que la primera fila esté disponible, en lugar de tener que esperar a que se rellene toda la tabla. También constituye una mejor alternativa si se devuelve un gran número de filas, ya que no tienen que materializarse en la memoria como un todo. Por ejemplo, puede utilizarse una función con valores de tabla administrada para analizar un archivo de texto y devolver cada línea como una fila.  
  
## <a name="implementing-table-valued-functions"></a>Implementar funciones con valores de tabla  
 Implemente las funciones con valores de tabla como métodos de una clase en un ensamblado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. El código de las funciones con valores de tabla debe implementar la interfaz `IEnumerable`. La interfaz `IEnumerable` se define en .NET Framework. Los tipos que representan matrices y colecciones en .NET Framework ya implementan la interfaz `IEnumerable`. De esta forma resulta más fácil escribir funciones con valores de tabla que conviertan una colección o una matriz en un conjunto de resultados.  
  
## <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 Los parámetros con valores de tabla son tipos de tabla definidos por el usuario que se pasan a un procedimiento o función, y proporcionan un modo eficaz de pasar varias filas de datos al servidor. Los parámetros con valores de tabla presentan una funcionalidad similar a la de las matrices de parámetros, pero proporcionan más flexibilidad y una mayor integración con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También proporcionan la posibilidad de obtener mayor rendimiento. Los parámetros con valores de tabla también ayudan a reducir el número de viajes de ida y vuelta (round trip) al servidor. En lugar de enviar varias solicitudes al servidor, como en el caso de una lista de parámetros escalares, los datos pueden enviarse al servidor como un parámetro con valores de tabla. Un tipo de tabla definido por el usuario no puede pasarse como un parámetro con valores de tabla a un procedimiento almacenado administrado o a una función que se ejecuta en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como tampoco puede devolverse desde dicho procedimiento o función. Para más información sobre los parámetros con valores de tabla, vea[Usar parámetros con valores de tabla &#40;motor de base de datos&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="output-parameters-and-table-valued-functions"></a>Parámetros de salida y funciones con valores de tabla  
 Se puede devolver información de funciones con valores de tabla mediante el uso de parámetros de salida. El parámetro correspondiente en el código de implementación de la función con valores de tabla debe usar un parámetro de paso por referencia como argumento. Tenga en cuenta que Visual Basic no admite parámetros de salida del mismo modo en que lo hace Visual C#. Debe especificar el parámetro por referencia y aplicar el \<atributo out () > para representar un parámetro de salida, como se muestra a continuación:  
  
```vb  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>Definir una función con valores de tabla en Transact-SQL  
 La sintaxis para definir una función con valores de tabla en CLR es similar a la de una función con valores de tabla de [!INCLUDE[tsql](../../includes/tsql-md.md)], con la adición de la cláusula `EXTERNAL NAME`. Por ejemplo:  
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 Las funciones con valores de tabla se utilizan para representar datos en formato relacional y procesarlos posteriormente en consultas como:  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 Las funciones con valores de tabla pueden devolver una tabla cuando:  
  
-   Se crean a partir de argumentos de entrada escalares. Por ejemplo, una función con valores de tabla que toma una cadena de números delimitados por comas y los dinamiza en una tabla.  
  
-   Se genera a partir de datos externos. Por ejemplo, una función con valores de tabla que lee el registro de eventos y lo expone como una tabla.  
  
 **Nota:** Una función con valores de tabla solo puede realizar el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] los datos a `InitMethod` través de una consulta en el `FillRow` método y no en el método. `InitMethod` debe marcarse con la propiedad de atributo `SqlFunction.DataAccess.Read` si se realiza una consulta [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="a-sample-table-valued-function"></a>A. Función con valores de tabla de ejemplo  
 La siguiente función con valores de tabla devuelve información del registro de eventos del sistema. La función toma un único argumento de cadena que contiene el nombre del registro de eventos que va a leerse.  
  
###### <a name="sample-code"></a>Código de ejemplo  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>Declarar y usar la función con valores de tabla de ejemplo  
 Una vea compilada la función con valores de tabla de ejemplo, puede declararse en [!INCLUDE[tsql](../../includes/tsql-md.md)] de la manera siguiente:  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 Los objetos de base de datos de Visual C++ compilados con /clr:pure no se admiten para la ejecución en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Por ejemplo, estos objetos de base de datos incluyen las funciones con valores de tabla.  
  
 Para probar el ejemplo, utilice el siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>Ejemplo: devolver los resultados de una consulta SQL Server  
 En el siguiente ejemplo se muestra una función con valores de tabla que consulta una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este ejemplo se utiliza la base de datos AdventureWorks Light de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Vea [https://www.codeplex.com/sqlserversamples](https://go.microsoft.com/fwlink/?LinkId=87843) para obtener más información acerca de la descarga de AdventureWorks.  
  
 Asigne a su archivo de código fuente el nombre FindInvalidEmails.cs o FindInvalidEmails.vb.  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 Compile el código fuente en una DLL y copie la DLL en el directorio raíz de su unidad C.  A continuación, ejecute la siguiente consulta [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
