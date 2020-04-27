---
title: Recuperando datos UDT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SqlDataReader object
- ADO.NET [CLR integration]
- binding UDTs [CLR integration]
- UDTs [CLR integration], ADO.NET
- assemblies [CLR integration], user-defined types
- query parameters [CLR integration]
- user-defined types [CLR integration], ADO.NET
- bytes [CLR integration]
ms.assetid: 6a98ac8c-0e69-4c03-83a4-2062cb782049
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085b1783214e7f629f1cb91084303edacd151c25
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874642"
---
# <a name="retrieving-udt-data"></a>Recuperar datos UDT
  Para crear un tipo definido por el usuario (UDT) en el cliente, el ensamblado que se registró como UDT en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar disponible para la aplicación cliente. El ensamblado UDT se puede colocar en el mismo directorio que la aplicación o en la caché de ensamblados global (GAC). También puede establecer una referencia al ensamblado en su proyecto.  
  
## <a name="requirements-for-using-udts-in-adonet"></a>Requisitos para utilizar UDT en ADO.NET  
 El ensamblado cargado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el ensamblado cargado en el cliente deben ser compatibles para que se pueda crear el UDT en el cliente. Para los UDT definidos con el formato de serialización `Native`, los ensamblados deben ser compatibles estructuralmente. En el caso de ensamblados definidos con el formato `UserDefined`, el ensamblado debe estar disponible en el cliente.  
  
 No es necesario que haya una copia del ensamblado UDT en el cliente para recuperar los datos sin formato de una columna UDT de una tabla.  
  
> [!NOTE]  
>  **SqlClient** puede no cargar un UDT en caso de que no coincidan las versiones UDT u otros problemas. En ese caso, utilice los mecanismos de solución de problemas habituales para determinar por qué la aplicación que realiza la llamada no encuentra el ensamblado que contiene el UDT. Para obtener más información, lea el tema denominado "Diagnóstico de errores con asistentes de depuraciones administradas" en la documentación de .NET Framework.  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>Obtener acceso a UDT con SqlDataReader  
 Se puede utilizar `System.Data.SqlClient.SqlDataReader` en el código del cliente para recuperar un conjunto de resultados que contiene una columna UDT, el cual se expone como una instancia del objeto.  
  
### <a name="example"></a>Ejemplo  
 En este ejemplo se muestra cómo utilizar el método `Main` para crear un nuevo objeto `SqlDataReader`.  En el ejemplo de código se producen las siguientes acciones:  
  
1.  El método Main crea un nuevo objeto `SqlDataReader` y recupera los valores de la tabla Points, que tiene una columna de UDT denominada Point.  
  
2.  El UDT Point expone las coordenadas X e Y definidas como enteros.  
  
3.  El UDT define un método `Distance` y un método `GetDistanceFromXY`.  
  
4.  El código muestra recupera los valores de las columnas de UDT y de clave principal para mostrar las capacidades del UDT.  
  
5.  El código muestra llama a los métodos `Point.Distance` y `Point.GetDistanceFromXY`.  
  
6.  Los resultados se muestran en la ventana de la consola.  
  
> [!NOTE]  
>  La aplicación ya debe tener una referencia al ensamblado UDT.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module ReadPoints  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the value of the UDT  
                Dim pnt As Point = CType(rdr(1), Point)  
  
             ' You can also use GetSqlValue and GetValue  
             ' Dim pnt As Point = CType(rdr.GetSqlValue(1), Point)  
             ' Dim pnt As Point = CType(rdr.GetValue(1), Point)  
  
                ' Print values  
                Console.WriteLine( _  
                 "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}", _  
                  id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance())  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
         & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
namespace Microsoft.Samples.SqlServer  
{  
class ReadPoints  
{  
static void Main()  
{  
  string connectionString = GetConnectionString();  
  using (SqlConnection cnn = new SqlConnection(connectionString))  
  {  
    cnn.Open();  
    SqlCommand cmd = new SqlCommand(  
       "SELECT ID, Pnt FROM dbo.Points", cnn);  
    SqlDataReader rdr = cmd.ExecuteReader();  
  
    while (rdr.Read())  
    {  
      // Retrieve the value of the Primary Key column  
      int id = rdr.GetInt32(0);  
  
        // Retrieve the value of the UDT  
        Point pnt = (Point)rdr[1];  
  
        // You can also use GetSqlValue and GetValue  
        // Point pnt = (Point)rdr.GetSqlValue(1);  
        // Point pnt = (Point)rdr.GetValue(1);  
  
        Console.WriteLine(  
        "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}",   
        id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance());  
    }  
  rdr.Close();  
  Console.WriteLine("done");  
  }  
  static private string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,   
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="binding-udts-as-bytes"></a>Enlazar UDT como bytes  
 Es posible que en algunas situaciones desee recuperar los datos sin formato de la columna de UDT. Quizás el tipo no esté disponible localmente o no desee crear instancias de una instancia del UDT. Puede leer los bytes sin formato en una matriz de bytes **GetBytes** mediante el método GetBytes `SqlDataReader`de un. Este método lee un flujo de bytes a partir del desplazamiento de la columna especificada en el búfer de una matriz, comenzando en el desplazamiento del búfer especificado. Otra opción es usar uno de los métodos **GetSqlBytes** o **GetSqlBinary** y leer todo el contenido en una sola operación. En cualquier caso, nunca se crean instancias del objeto UDT, de modo que no es necesario establecer una referencia al UDT en el ensamblado de cliente.  
  
### <a name="example"></a>Ejemplo  
 En este ejemplo se muestra cómo recuperar los datos de **punto** como bytes sin formato en una matriz `SqlDataReader`de bytes mediante. El código utiliza `System.Text.StringBuilder` para convertir los bytes sin formato en una representación de cadena que se mostrará en la ventana de la consola.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the raw bytes into a byte array  
                Dim buffer(31) As Byte  
                Dim byteCount As Integer = _  
                 CInt(rdr.GetBytes(1, 0, buffer, 0, 31))  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", buffer(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
        string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand("SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Retrieve the raw bytes into a byte array  
                byte[] buffer = new byte[32];  
                long byteCount = rdr.GetBytes(1, 0, buffer, 0, 32);  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", buffer[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
### <a name="example-using-getsqlbytes"></a>Ejemplo con GetSqlBytes  
 En este ejemplo se muestra cómo recuperar los datos de **punto** como bytes sin formato en una sola operación mediante el método **GetSqlBytes** . El código utiliza `StringBuilder` para convertir los bytes sin formato en una representación de cadena que se mostrará en la ventana de la consola.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Use SqlBytes to retrieve raw bytes  
                Dim sb As SqlBytes = rdr.GetSqlBytes(1)  
                Dim byteCount As Long = sb.Length  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", sb(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
         string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Use SqlBytes to retrieve raw bytes  
                SqlBytes sb = rdr.GetSqlBytes(1);  
                long byteCount = sb.Length;  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", sb[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="working-with-udt-parameters"></a>Trabajar con parámetros UDT  
 Los UDT se pueden utilizar en el código de ADO.NET como parámetros de entrada y de salida.  
  
## <a name="using-udts-in-query-parameters"></a>Utilizar UDT en parámetros de consulta  
 Los UDT se pueden utilizar como valores de parámetros cuando se configura un `SqlParameter` para un objeto `System.Data.SqlClient.SqlCommand`. La enumeración `SqlDbType.Udt` de un objeto `SqlParameter` se utiliza para indicar que el parámetro es un UDT cuando se llama al método `Add` en la colección `Parameters`. La `UdtTypeName` propiedad de un `SqlCommand` objeto se utiliza para especificar el nombre completo del UDT en la base de datos utilizando la sintaxis *Database. schema_name. object_name* . Aunque no es necesario, el uso del nombre completo quita ambigüedad al código.  
  
> [!NOTE]  
>  Debe haber una copia local del ensamblado UDT disponible para el proyecto del cliente.  
  
### <a name="example"></a>Ejemplo  
 El código de este ejemplo crea objetos `SqlCommand` y `SqlParameter` para insertar datos en una columna de UDT de una tabla. El código utiliza la enumeración `SqlDbType.Udt` para especificar el tipo de datos y la propiedad `UdtTypeName` del objeto `SqlParameter` para especificar el nombre completo del UDT en la base de datos.  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports system.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim ConnectionString As String = GetConnectionString()  
    Dim cnn As New SqlConnection(ConnectionString)  
    Using cnn  
      Dim cmd As SqlCommand = cnn.CreateCommand()  
      cmd.CommandText = "INSERT INTO dbo.Points (Pnt) VALUES (@Point)"  
      cmd.CommandType = CommandType.Text  
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      param.UdtTypeName = "TestPoint.dbo.Point"      param.Direction = ParameterDirection.Input      param.Value = New Point(5, 6)      cmd.Parameters.Add(param)  
  
      cnn.Open()  
      cmd.ExecuteNonQuery()  
      Console.WriteLine("done")  
    End Using  
  End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  string ConnectionString = GetConnectionString();  
     using (SqlConnection cnn = new SqlConnection(ConnectionString))  
     {  
       SqlCommand cmd = cnn.CreateCommand();  
       cmd.CommandText =   
         "INSERT INTO dbo.Points (Pnt) VALUES (@Point)";  
       cmd.CommandType = CommandType.Text;  
  
       SqlParameter param = new SqlParameter("@Point", SqlDbType.Udt);       param.UdtTypeName = "TestPoint.dbo.Point";       param.Direction = ParameterDirection.Input;       param.Value = new Point(5, 6);       cmd.Parameters.Add(param);  
  
       cnn.Open();  
       cmd.ExecuteNonQuery();  
       Console.WriteLine("done");  
     }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Acceso a tipos definidos por el usuario en ADO.NET](accessing-user-defined-types-in-ado-net.md)  
  
  
