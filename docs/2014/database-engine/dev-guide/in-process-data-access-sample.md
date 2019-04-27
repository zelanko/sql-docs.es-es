---
title: Ejemplo de acceso a datos en proceso | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 155be272-4f9a-4d86-9f4f-714c4f45b49a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9854218e66d3edfe10f4220a5ac662cccc6f481
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62781143"
---
# <a name="in-process-data-access-sample"></a>Ejemplo de acceso a datos en proceso
  El ejemplo `InProcessDataAccess` contiene una serie de funciones simples que muestran diversas características del proveedor de acceso a datos en proceso de CLR de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para crear y ejecutar este proyecto se debe instalar el siguiente software:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express. Puede obtener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express de forma gratuita desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio web [de documentación y ejemplos de](https://go.microsoft.com/fwlink/?LinkId=31046)Express.  
  
-   La base de datos de AdventureWorks que está disponible en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio web [para desarrolladores de](https://go.microsoft.com/fwlink/?linkid=62796).  
  
-   .NET Framework SDK 2.0 o posterior, o Microsoft Visual Studio 2005 o posterior. Puede obtener .NET Framework SDK de forma gratuita.  
  
-   Además, se deben cumplir las siguientes condiciones:  
  
-   La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando debe tener habilitada la integración con CLR.  
  
-   Para habilitar la integración con CLR, siga estos pasos:  
  
    #### <a name="enabling-clr-integration"></a>Habilitar la integración con CLR  
  
    -   Ejecute los siguientes comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  Para habilitar CLR, debe tener el permiso de nivel de servidor `ALTER SETTINGS`, que se concede implícitamente a los miembros de los roles fijos de servidor `sysadmin` y `serveradmin`.  
  
-   La base de datos de AdventureWorks debe estar instalada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando.  
  
-   Si no es administrador de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está utilizando, debe hacer que un administrador le conceda el permiso **CreateAssembly** para completar la instalación.  
  
## <a name="building-the-sample"></a>Generar el ejemplo  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>Cree y ejecute el ejemplo utilizando las siguientes instrucciones:  
  
1.  Abra un símbolo del sistema de Visual Studio o de .NET Framework.  
  
2.  Si es necesario, cree un directorio para el ejemplo. Para este ejemplo, utilizaremos C:\MySample.  
  
3.  En c:\MySample, cree `inprocda.vb` (para el ejemplo de Visual Basic) o `inprocda.cs` (para el ejemplo de C#) y copie el código muestra de Visual Basic o de C# que corresponda (más abajo) en el archivo.  
  
4.  Compile el código muestra en el ensamblado requerido ejecutando en el símbolo del sistema uno de los comandos siguientes, dependiendo de su opción de lenguaje.  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library InProcDA.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /target:library inprocda.cs`  
  
5.  Copie el código de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `Install.sql` en el directorio de ejemplo.  
  
6.  Si el ejemplo está instalado en un directorio distinto de `C:\MySample\`, edite el archivo `Install.sql` del archivo como se indica para señalar esa ubicación.  
  
7.  Implemente el ensamblado, el procedimiento almacenado y las funciones ejecutando  
  
    -   `sqlcmd -E -I -i install.sql`  
  
8.  Copie el código de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `test.sql` en el directorio de ejemplo.  
  
9. Pruebe la aplicación ejecutando la siguiente línea en el símbolo del sistema:  
  
    -   `sqlcmd -E -I -i test.sql`  
  
10. Copie el script de limpieza de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `cleanup.sql` en el directorio de ejemplo.  
  
11. Ejecute el script con el siguiente comando  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>Código muestra  
 A continuación se muestran las listas de código para este ejemplo.  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
public sealed class DataAccessDemo  
{  
        private DataAccessDemo()  
        {  
        }  
  
        /// <summary>  
/// Simple example to send a message to the client.  
/// </summary>  
public static void SendMessage(string msg)  
{  
SqlContext.Pipe.Send("Message from server: " + msg);  
}  
  
/// <summary>  
/// Simple example of performing data access within  
/// a function  
/// </summary>  
/// <returns></returns>  
        [Microsoft.SqlServer.Server.SqlFunction(DataAccess = Microsoft.SqlServer.Server.DataAccessKind.Read)]  
public static string ReportSqlVersion()  
{  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
                //create a command from the current context  
                SqlCommand cmd = conn.CreateCommand();  
  
                //execute something  
                cmd.CommandText = "select @@version";  
  
                conn.Open();  
                //return results as scalar  
                return (string)cmd.ExecuteScalar();  
            }  
}  
  
/// <summary>  
/// Create a result set on the fly and send it to the client.  
/// </summary>  
public static void SendTransientResultSet()  
{  
//create the metadata for the columns  
            Microsoft.SqlServer.Server.SqlMetaData[] columnSchema   
                = new Microsoft.SqlServer.Server.SqlMetaData[] {  
new Microsoft.SqlServer.Server.SqlMetaData("stringcol", SqlDbType.NVarChar, 128)  
};  
  
//create a record based on that metadata  
            SqlDataRecord newRecord = new SqlDataRecord(columnSchema);  
  
//populate it  
newRecord.SetString(0, "Hello World!");  
  
//send it  
SqlContext.Pipe.Send(newRecord);  
}  
  
/// <summary>  
/// Execute a command and send the results to the client directly.  
/// </summary>  
public static void ExecuteToClient()  
{  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
                SqlCommand cmd = conn.CreateCommand();  
  
                cmd.CommandText = "select @@version";  
                conn.Open();  
                SqlContext.Pipe.ExecuteAndSend(cmd);  
            }  
}  
  
/// <summary>  
/// Execute a command and send the resultig reader to the client  
/// </summary>  
public static void SendReaderToClient()  
{  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
                SqlCommand cmd = conn.CreateCommand();  
  
                cmd.CommandText = "select @@version";  
                conn.Open();  
                SqlDataReader rdr = cmd.ExecuteReader();  
                try  
                {  
                    SqlContext.Pipe.Send(rdr);  
                }  
                finally  
                {  
                    rdr.Close();  
                }  
            }  
}  
  
};  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Partial Public NotInheritable Class DataAccessDemo  
    Private Sub New()  
    End Sub  
  
    ''' <summary>  
    ''' Simple example of performing data access within a function  
    ''' </summary>  
    ''' <returns></returns>  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReportSqlVersion() As SqlString  
        Using conn As New SqlConnection("context connection=true")  
            'create a command from the current context  
            Dim cmd As SqlCommand = conn.CreateCommand()  
  
            'execute something  
            cmd.CommandText = "SELECT @@VERSION"  
  
            conn.Open()  
  
            'return results as scalar  
            Return CType(cmd.ExecuteScalar(), String)  
        End Using  
    End Function  
  
    ''' <summary>  
    ''' Simple example to send a message to the client.  
    ''' </summary>  
    Public Shared Sub SendMessage(ByVal msg As String)  
        SqlContext.Pipe.Send(("Message from server: " & msg))  
    End Sub  
  
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    Public Shared Sub SendTransientResultSet()  
        'create the metadata for the columns  
        Dim columnSchema() As Microsoft.SqlServer.Server.SqlMetaData _  
            = {New SqlMetaData("stringcol", SqlDbType.NVarChar, 128)}  
  
        'create a record based on that metadata  
        Dim newRecord As New SqlDataRecord(columnSchema)  
  
        'populate it  
        newRecord.SetString(0, "Hello World!")  
  
        'send it  
        SqlContext.Pipe.Send(newRecord)  
    End Sub  
  
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    Public Shared Sub ExecuteToClient()  
        Using conn As New SqlConnection("context connection=true")  
            Dim cmd As SqlCommand = conn.CreateCommand()  
  
            cmd.CommandText = "SELECT @@VERSION"  
            conn.Open()  
            SqlContext.Pipe.ExecuteAndSend(cmd)  
        End Using  
    End Sub  
  
    ''' <summary>  
    ''' Execute a command and send the resulting reader to the client  
    ''' </summary>  
    Public Shared Sub SendReaderToClient()  
        Using conn As New SqlConnection("context connection=true")  
            Dim cmd As SqlCommand = conn.CreateCommand()  
            cmd.CommandText = "SELECT @@VERSION"  
            conn.Open()  
            Dim rdr As SqlDataReader = cmd.ExecuteReader()  
            Try  
                SqlContext.Pipe.Send(rdr)  
            Finally  
                rdr.Close()  
            End Try  
        End Using  
    End Sub  
  
End Class  
  
```  
  
 Este es el script de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] (`Install.sql`), que implementa el ensamblado y crea los procedimientos almacenados y la función requeridos por este ejemplo.  
  
```  
USE AdventureWorks;  
GO  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'SendMessage')  
DROP PROCEDURE SendMessage;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'SendTransientResultSet')  
DROP PROCEDURE SendTransientResultSet;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'ExecuteToClient')  
DROP PROCEDURE ExecuteToClient;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'SendReaderToClient')  
DROP PROCEDURE SendReaderToClient;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE name = N'ReportSqlVersion' and (type = 'FS' or type = 'FT'))    
DROP FUNCTION [ReportSqlVersion];  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'InProcDA') DROP ASSEMBLY InProcDA;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
set @SamplesPath = N'C:\MySample\'  
CREATE ASSEMBLY InProcDA FROM @SamplesPath + 'InProcDA.dll'  
WITH permission_set = SAFE;  
GO  
  
CREATE PROCEDURE [SendMessage] @msg nvarchar(4000)  
AS  
EXTERNAL NAME [InProcDA].[DataAccessDemo].[SendMessage];  
GO  
  
CREATE FUNCTION [ReportSqlVersion]() RETURNS nvarchar(4000)  
AS EXTERNAL NAME [InProcDA].[DataAccessDemo].[ReportSqlVersion];  
GO  
  
CREATE PROCEDURE [SendTransientResultSet]  
AS  
EXTERNAL NAME [InProcDA].[DataAccessDemo].[SendTransientResultSet];  
GO  
  
CREATE PROCEDURE [ExecuteToClient]  
AS  
EXTERNAL NAME [InProcDA].[DataAccessDemo].[ExecuteToClient];  
GO  
  
CREATE PROCEDURE [SendReaderToClient]  
AS  
EXTERNAL NAME [InProcDA].[DataAccessDemo].[SendReaderToClient];  
GO  
```  
  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] (`test.sql`) prueba el ejemplo ejecutando los procedimientos almacenados y la función definida en este ejemplo.  
  
```  
USE AdventureWorks;  
GO  
  
-- send a message to the client  
EXEC SendMessage  N'This is a test message.';  
  
-- exec a function that does data access  
SELECT dbo.ReportSqlVersion();  
  
-- exec the proc that sends a result set to the client  
EXEC SendTransientResultSet;  
  
EXEC ExecuteToClient;  
  
EXEC SendReaderToClient;  
  
USE master;  
GO  
  
```  
  
 El siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] quita de la base de datos el ensamblado, la función y los procedimientos almacenados.  
  
```  
  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'SendMessage')  
DROP PROCEDURE SendMessage;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'SendTransientResultSet')  
DROP PROCEDURE SendTransientResultSet;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'ExecuteToClient')  
DROP PROCEDURE ExecuteToClient;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE name = N'SendReaderToClient')  
DROP PROCEDURE SendReaderToClient;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE name = N'ReportSqlVersion' and (type = 'FS' or type = 'FT'))    
DROP FUNCTION [ReportSqlVersion];  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'InProcDA') DROP ASSEMBLY InProcDA;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de uso y ejemplos para la integración de Common Language Runtime &#40;CLR&#41;](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
