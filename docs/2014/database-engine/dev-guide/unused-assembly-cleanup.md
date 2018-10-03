---
title: Limpieza de ensamblado sin usar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
ms.assetid: e03c2b6f-8f39-4382-9cf3-7f766a1bd929
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad8d959ae622d743de02d996c280af37eddc9bf2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184085"
---
# <a name="unused-assembly-cleanup"></a>Limpieza del ensamblado sin usar
  El ejemplo `AssemblyCleanup` contiene un procedimiento almacenado de .NET que limpia los ensamblados no usados en la base de datos actual mediante consultas en los catálogos de metadatos. Su único parámetro, `visible_assemblies`, se utiliza para especificar si se deben quitar los ensamblados visibles no usados o no. Un valor de 'false' significa de forma predeterminada que solo se quitarán los ensamblados no visibles no usados; en los demás casos se quitarán todos los ensamblados no usados. El conjunto de ensamblados no usados está formado por aquellos que no tienen ningún punto de entrada definido (rutinas, tipos y agregados) y que no tienen ningún ensamblado utilizado que haga referencia a ellos directa o indirectamente.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para crear y ejecutar este proyecto se debe instalar el siguiente software:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express. Puede obtener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express de forma gratuita desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio web [de documentación y ejemplos de](http://go.microsoft.com/fwlink/?LinkId=31046)Express.  
  
-   La base de datos de AdventureWorks que está disponible en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sitio web [para desarrolladores de](http://go.microsoft.com/fwlink/?linkid=62796).  
  
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
    >  Para habilitar CLR, debe tener `ALTER SETTINGS` permiso de nivel de servidor, que se concede implícitamente a los miembros de la `sysadmin` y `serveradmin` roles fijos de servidor.  
  
-   La base de datos de AdventureWorks debe estar instalada en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando.  
  
-   Si no es administrador de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está usando, debe hacer que un administrador le conceda el permiso **CreateAssembly**  para completar la instalación.  
  
## <a name="building-the-sample"></a>Generar el ejemplo  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>Cree y ejecute el ejemplo utilizando las siguientes instrucciones:  
  
1.  Abra un símbolo del sistema de Visual Studio o de .NET Framework.  
  
2.  Si es necesario, cree un directorio para el ejemplo. Para este ejemplo, utilizaremos C:\MySample.  
  
3.  En c:\MySample, cree `AssemblyCleanup.vb` (para el ejemplo de Visual Basic) o `AssemblyCleanup.cs` (para el ejemplo de C#) y copie el código muestra de Visual Basic o de C# que corresponda (más abajo) en el archivo.  
  
4.  Compile el código muestra desde el símbolo del sistema ejecutando uno de los comandos siguientes, dependiendo de su opción de lenguaje.  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Transactions.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library AssemblyCleanup.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /target:library AssemblyCleanup.cs`  
  
5.  Copie el código de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `Install.sql` en el directorio de ejemplo.  
  
6.  Si el ejemplo está instalado en un directorio distinto de `C:\MySample\`, edite el archivo `Install.sql` del archivo como se indica para señalar esa ubicación.  
  
7.  Implemente el ensamblado y el procedimiento almacenado ejecutando  
  
    -   `sqlcmd -E -I -i install.sql`  
  
8.  Copie el script de comando de prueba de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `test.sql` en el directorio de ejemplo.  
  
9. Ejecute el script de prueba con el siguiente comando  
  
    -   `sqlcmd -E -I -i test.sql`  
  
10. Copie el script de limpieza de [!INCLUDE[tsql](../../includes/tsql-md.md)] en un archivo y guárdelo como `cleanup.sql` en el directorio de ejemplo.  
  
11. Ejecute el script con el siguiente comando  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>Código muestra  
 A continuación se muestran las listas de código para este ejemplo.  
  
 C#  
  
```  
using System;  
using System.Text;  
using System.Diagnostics;  
using System.Data.SqlClient;  
using System.Collections.Generic;  
using System.Globalization;  
using Microsoft.SqlServer.Server;  
  
    /// <summary>  
    /// Defines a CLR user defined function CleanupUnusedAssemblies that drops   
    /// all the invisible assemblies with no references.  
    /// </summary>  
    public sealed class AssemblyCleanup  
    {  
        private SqlTransaction transaction;  
  
        internal class AssemblySet  
        {  
            private Dictionary<int, object> m_dictionary;  
  
            /// <summary>  
            /// Initialize internal structures  
            /// </summary>  
            /// <returns></returns>  
            public AssemblySet()  
            {  
                m_dictionary = new Dictionary<int, object>();  
            }  
  
            /// <summary>  
            /// Adds an assembly id into the current AssemblySet if it is not   
            /// already part of it.  
            /// </summary>  
            /// <returns></returns>  
            public void Add(int assemblyId)  
            {  
                if (!m_dictionary.ContainsKey(assemblyId))  
                {  
                    m_dictionary.Add(assemblyId, null);  
                }  
            }  
  
            /// <summary>  
            /// Number of assembly ids stored in this instance  
            /// </summary>  
            /// <returns></returns>  
            public int Count  
            {  
                get  
                {  
                    return m_dictionary.Count;  
                }  
            }  
  
            /// <summary>  
            /// Returns the comma-separated list of assembly ids contained in this instance  
            /// </summary>  
            /// <returns>string value that represents a comma-seperated list   
            /// of assembly ids</returns>  
            public string ToCommaSeperatedList()  
            {  
                StringBuilder sb = new StringBuilder();  
  
                if (m_dictionary.Count > 0)  
                {  
                    foreach (KeyValuePair<int, object> kv in m_dictionary)  
                    {  
                        sb.Append(kv.Key);  
                        sb.Append(",");  
                    }  
  
                    sb.Length--; // remove the trailing comma  
                }  
  
                return sb.ToString();  
            }  
        }  
  
        /// <summary>  
        /// Initializes an instance of AssemblyCleanup with a SqlTransaction  
        /// </summary>  
        /// <returns></returns>  
        private AssemblyCleanup(SqlTransaction transaction)  
        {  
            this.transaction = transaction;  
        }  
  
        /// <summary>  
        /// Helper function that creates a SqlCommand object as part of the current   
        /// transaction  
        /// </summary>  
        /// <returns></returns>  
        private SqlCommand CreateCommandInTransaction()  
        {  
            SqlCommand cmd = this.transaction.Connection.CreateCommand();  
  
            cmd.Transaction = this.transaction;  
  
            return cmd;  
        }  
  
        /// <summary>  
        /// Helper function that constructs an AssemblySet instance using the   
        /// first column of the resultset resulting from the query that was passed in.  
        /// </summary>  
        /// <param name="query"></param>  
        /// <returns></returns>  
        private AssemblySet GetAssemblySetFromQuery(string query)  
        {  
            SqlCommand cmd = CreateCommandInTransaction();  
  
            AssemblySet set = new AssemblySet();  
  
            cmd.CommandText = query;  
            using (SqlDataReader rd = cmd.ExecuteReader())  
            {  
                while (rd.Read())  
                {  
                    set.Add(rd.GetInt32(0));  
                }  
            }  
  
            return set;  
        }  
  
        /// <summary>  
        /// Constructs a DROP ASSEMBLY T-SQL statement using the AssemblySet   
        /// passed in as a parameter.  
        /// </summary>  
        /// <param name="set"></param>  
        /// <returns></returns>  
        private void DropAssemblies(AssemblySet unusedAssemblySet)  
        {  
            if (unusedAssemblySet.Count > 0)  
            {  
                StringBuilder assemblyNamesToDrop = new StringBuilder();  
  
                // Gather the list of assembly names we will drop later  
                SqlCommand cmd = CreateCommandInTransaction();  
  
                cmd.CommandText = String.Format(CultureInfo.InvariantCulture,  
                    "SELECT name FROM sys.assemblies WHERE assembly_id IN ({0});",  
                    unusedAssemblySet.ToCommaSeperatedList());  
                using (SqlDataReader rd = cmd.ExecuteReader())  
                {  
                    while (rd.Read())  
                    {  
                        assemblyNamesToDrop.Append("[");  
                        assemblyNamesToDrop.Append(rd.GetString(0));  
                        assemblyNamesToDrop.Append("],");  
                    }  
                }  
  
                // Remove trailing comma  
                assemblyNamesToDrop.Length--;  
  
                // Drop all assemblies at the same time  
                cmd.CommandText = String.Format(CultureInfo.InvariantCulture,  
                    "DROP ASSEMBLY {0}", assemblyNamesToDrop.ToString());  
                cmd.ExecuteNonQuery();  
            }  
        }  
  
        /// <summary>  
        /// Serves as the stored procedure entry point and drives the process   
        /// of expanding the "assemblies in use" set, negating it, and   
        /// dropping the results  
        /// </summary>  
        /// <param name="visibleAssemblies">If set to true, will also drop   
        /// unused visible assemblies. Otherwise, will only drop unused invisible   
        /// assemblies.</param>  
        /// <returns></returns>  
        [Microsoft.SqlServer.Server.SqlProcedure()]  
        public static void CleanupUnusedAssemblies(bool visibleAssemblies)  
        {  
            bool succeeded = false;  
            SqlConnection conn;  
            SqlTransaction transaction;  
            string sqlStatement;  
            AssemblySet assembliesToDrop;  
            AssemblyCleanup assemblyCleanup;  
  
            conn = new SqlConnection("context connection=true");  
            conn.Open();  
            transaction = conn.BeginTransaction();  
  
            try  
            {  
                // Create a set of assemblies in use by looking at   
                // the metadata of the current database  
                sqlStatement =  
                    "DECLARE @UsedAssembly TABLE (AssemblyID int NOT NULL); " +  
                    "DECLARE @RowCount int; " +  
                    "INSERT INTO @UsedAssembly " +  
                    "SELECT DISTINCT([assembly_id]) " +  
                    "FROM sys.assembly_modules " +  
                    "UNION " +  
                    "SELECT [assembly_id] " +  
                    "FROM sys.assembly_types; " +  
                    "SET @RowCount = @@ROWCOUNT; " +  
                    "WHILE @RowCount > 0 " +  
                    "BEGIN " +  
                    "INSERT INTO @UsedAssembly " +  
                    "SELECT [referenced_assembly_id] " +  
                    "FROM sys.assembly_references ar " +  
                    "INNER JOIN @UsedAssembly ua " +  
                    "ON ar.[assembly_id] = ua.AssemblyID " +  
                    "WHERE NOT EXISTS (SELECT * FROM @UsedAssembly WHERE AssemblyID = [referenced_assembly_id]) " +  
                    "SET @RowCount = @@ROWCOUNT; " +  
                    "END;";  
  
                if (visibleAssemblies)  
                {  
                    sqlStatement +=  
                        "SELECT assembly_id " +  
                        "FROM sys.assemblies " +  
                        "WHERE assembly_id NOT IN (SELECT AssemblyID FROM @UsedAssembly);";  
                }  
                else  
                {  
                    sqlStatement +=  
                        "SELECT assembly_id " +  
                        "FROM sys.assemblies " +  
                        "WHERE assembly_id NOT IN (SELECT AssemblyID FROM @UsedAssembly) " +  
                        "    AND is_visible = 0;";  
                }  
  
                // This marks the beginning of the transaction  
                assemblyCleanup = new AssemblyCleanup(transaction);  
  
                // Assemblies that are currently in use  
                assembliesToDrop  
                    = assemblyCleanup.GetAssemblySetFromQuery(sqlStatement);  
  
                assemblyCleanup.DropAssemblies(assembliesToDrop);  
  
                // Mark as succeeded  
                succeeded = true;  
            }  
            finally  
            {  
                // We must guarantee that we explicitly call either Commit()   
                // or Rollback() before we return.  
                if (succeeded)  
                {  
                    transaction.Commit();  
                }  
                else  
                {  
                    transaction.Rollback();  
                }  
                conn.Dispose();  
            }  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System  
Imports System.Collections  
Imports System.Collections.Generic  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Diagnostics  
Imports System.Globalization  
Imports System.Text  
Imports System.Transactions  
Public NotInheritable Class AssemblyCleanup  
    Private transaction As SqlTransaction  
  
    Friend Class AssemblySet  
        Private m_dictionary As Dictionary(Of Integer, Object)  
  
        ''' <summary>  
        ''' Initialize internal structures  
        ''' </summary>  
        ''' <returns></returns>  
        Public Sub New()  
            m_dictionary = New Dictionary(Of Integer, Object)  
        End Sub  
  
        ''' <summary>  
        ''' Adds an assembly id into the current AssemblySet if it is not already part of it.  
        ''' </summary>  
        ''' <returns></returns>  
        Public Sub Add(ByVal assemblyId As Integer)  
            If Not m_dictionary.ContainsKey(assemblyId) Then  
                m_dictionary.Add(assemblyId, Nothing)  
            End If  
        End Sub  
  
        ''' <summary>  
        ''' Number of assembly ids stored in this instance  
        ''' </summary>  
        ''' <returns></returns>  
        Public ReadOnly Property Count() As Integer  
            Get  
                Return m_dictionary.Count  
            End Get  
        End Property  
  
        ''' <summary>  
        ''' Returns the comma-separated list of assembly ids contained in this instance  
        ''' </summary>  
        ''' <returns>string value that represents a comma-seperated list of assembly ids</returns>  
        Public Function ToCommaSeperatedList() As String  
            Dim sb As New StringBuilder()  
  
            If m_dictionary.Count > 0 Then  
                For Each kv As KeyValuePair(Of Integer, Object) In m_dictionary  
                    If (True) Then  
                        sb.Append(kv.Key)  
                        sb.Append(",")  
                    End If  
                Next  
  
                sb.Length -= 1 ' remove the trailing comma  
            End If  
  
            Return sb.ToString()  
  
        End Function  
    End Class  
  
    ''' <summary>  
    ''' Initializes an instance of AssemblyCleanup with a SqlTransaction  
    ''' </summary>  
    ''' <returns></returns>  
    Private Sub New(ByVal trans As SqlTransaction)  
        Me.transaction = trans  
    End Sub  
  
    ''' <summary>  
    ''' Helper function that creates a SqlCommand object as part of the   
    ''' current transaction  
    ''' </summary>  
    ''' <returns></returns>  
    Private Function CreateCommandInTransaction() As SqlCommand  
        Dim cmd As SqlCommand = transaction.Connection.CreateCommand()  
  
        cmd.Transaction = Me.transaction  
  
        Return cmd  
    End Function  
  
    ''' <summary>  
    ''' Helper function that constructs an AssemblySet instance using the   
    ''' first column of the resultset resulting from the query that was passed in.  
    ''' </summary>  
    ''' <param name="query"></param>  
    ''' <returns></returns>  
    Private Function GetAssemblySetFromQuery(ByVal query As String) As AssemblySet  
        Dim cmd As SqlCommand = CreateCommandInTransaction()  
        Dim [set] As New AssemblySet()  
  
        cmd.CommandText = query  
        Dim rd As SqlDataReader = cmd.ExecuteReader()  
        Try  
            While rd.Read()  
                [set].Add(rd.GetInt32(0))  
            End While  
        Finally  
            rd.Dispose()  
        End Try  
  
        Return [set]  
    End Function  
  
    ''' <summary>  
    ''' Constructs a DROP ASSEMBLY T-SQL statement using the AssemblySet   
    ''' passed in as a parameter.  
    ''' </summary>  
    ''' <param name="set"></param>  
    ''' <returns></returns>  
    Private Sub DropAssemblies(ByVal unusedAssemblySet As AssemblySet)  
        If unusedAssemblySet.Count > 0 Then  
            Dim assemblyNamesToDrop As New StringBuilder()  
  
            ' Gather the list of assembly names we will drop later  
            Dim cmd As SqlCommand = CreateCommandInTransaction()  
  
            cmd.CommandText = String.Format(CultureInfo.InvariantCulture, _  
                "SELECT name FROM sys.assemblies WHERE assembly_id IN ({0});", _  
                unusedAssemblySet.ToCommaSeperatedList())  
            Dim rd As SqlDataReader = cmd.ExecuteReader()  
            Try  
                While rd.Read()  
                    assemblyNamesToDrop.Append("[")  
                    assemblyNamesToDrop.Append(rd.GetString(0))  
                    assemblyNamesToDrop.Append("],")  
                End While  
            Finally  
                rd.Dispose()  
            End Try  
  
            ' Remove trailing comma  
            assemblyNamesToDrop.Length -= 1  
  
            ' Drop all assemblies at the same time  
            cmd.CommandText = String.Format(CultureInfo.InvariantCulture, _  
                "DROP ASSEMBLY {0}", assemblyNamesToDrop.ToString())  
            cmd.ExecuteNonQuery()  
        End If  
    End Sub  
  
    ''' <summary>  
    ''' Serves as the stored procedure entry point and drives the process of   
    ''' expanding the "assemblies in use" set, negating it, and dropping   
    ''' the results.  
    ''' </summary>  
    ''' <param name="visibleAssemblies">If set to true, will also drop unused   
    ''' visible assemblies. Otherwise, will only drop unused invisible assemblies.</param>  
    ''' <returns></returns>  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub CleanupUnusedAssemblies(ByVal visibleAssemblies As Boolean)  
  
        Dim succeeded As Boolean = False  
        Dim conn As SqlConnection  
        Dim transaction As SqlTransaction  
        Dim sqlStatement As String  
        Dim assembliesToDrop As AssemblySet  
        Dim assemblyCleanup As AssemblyCleanup  
  
        conn = New SqlConnection("context connection=true")  
        conn.Open()  
        transaction = conn.BeginTransaction()  
  
        Try  
            ' Create a set of assemblies in use by looking at   
            ' the metadata of the current database  
            sqlStatement = "DECLARE @UsedAssembly TABLE (AssemblyID int NOT NULL); " & _  
                "DECLARE @RowCount int; " & _  
                "INSERT INTO @UsedAssembly " & _  
                "SELECT DISTINCT([assembly_id]) " & _  
                "FROM sys.assembly_modules " & _  
                "UNION " & _  
                "SELECT [assembly_id] " & _  
                "FROM sys.assembly_types; " & _  
                "SET @RowCount = @@ROWCOUNT; " & _  
                "WHILE @RowCount > 0 " & _  
                "BEGIN " & _  
                "INSERT INTO @UsedAssembly " & _  
                "SELECT [referenced_assembly_id] " & _  
                "FROM sys.assembly_references ar " & _  
                "INNER JOIN @UsedAssembly ua " & _  
                "ON ar.[assembly_id] = ua.AssemblyID " & _  
                "WHERE NOT EXISTS (SELECT * FROM @UsedAssembly WHERE AssemblyID = [referenced_assembly_id]) " & _  
                "SET @RowCount = @@ROWCOUNT; " & _  
                "END;"  
  
            If visibleAssemblies Then  
                sqlStatement += "SELECT assembly_id " & _  
                    "FROM sys.assemblies " & _  
                    "WHERE assembly_id NOT IN (SELECT AssemblyID FROM @UsedAssembly);"  
            Else  
                sqlStatement += "SELECT assembly_id " & _  
                    "FROM sys.assemblies " & _  
                    "WHERE assembly_id NOT IN (SELECT AssemblyID FROM @UsedAssembly) " & _  
                    "    AND is_visible = 0;"  
            End If  
  
            ' This marks the beginning of the transaction  
            assemblyCleanup = New AssemblyCleanup(transaction)  
  
            ' Assemblies that are currently in use  
            assembliesToDrop _  
                = assemblyCleanup.GetAssemblySetFromQuery(sqlStatement)  
  
            assemblyCleanup.DropAssemblies(assembliesToDrop)  
  
            ' Mark as succeeded  
            succeeded = True  
        Finally  
            ' We must guarantee that we explicitly call either Commit()   
            ' or Rollback() before we return.  
            If succeeded Then  
                transaction.Commit()  
            Else  
                transaction.Rollback()  
            End If  
            conn.Dispose()  
        End Try  
    End Sub  
End Class  
```  
  
 Este es el script de instalación de [!INCLUDE[tsql](../../includes/tsql-md.md)] (`Install.sql`), que implementa el ensamblado y crea el procedimiento almacenado en la base de datos.  
  
```  
USE AdventureWorks;  
GO  
IF EXISTS (SELECT * FROM sys.objects WHERE name = N'CleanupUnusedAssemblies')  
DROP PROCEDURE CleanupUnusedAssemblies;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'AssemblyCleanupUtils')   
DROP ASSEMBLY AssemblyCleanupUtils;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
  
-- You may need to modify the value of the this variable if you have installed the sample someplace other than the default location.  
Set @SamplesPath = 'C:\MySample\'  
  
CREATE ASSEMBLY AssemblyCleanupUtils   
FROM @SamplesPath + 'AssemblyCleanup.dll'   
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE CleanupUnusedAssemblies (  
@visible_assemblies bit  
) AS  
EXTERNAL NAME [AssemblyCleanupUtils].[AssemblyCleanup].CleanupUnusedAssemblies;  
GO  
```  
  
 Este es el script `test.sql`, que prueba el ejemplo ejecutando el procedimiento almacenado.  
  
```  
USE AdventureWorks;  
GO  
  
PRINT 'Before cleanup...'  
SELECT [name] FROM sys.assemblies;  
GO  
  
-- pass in false, which means the cleanup will only include invisible assemblies  
EXEC dbo.CleanupUnusedAssemblies false;  
GO  
  
PRINT 'After cleanup'  
SELECT [name] FROM sys.assemblies;  
```  
  
 El script [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente quita el ensamblado y el procedimiento almacenado de la base de datos.  
  
```  
USE AdventureWorks;  
GO  
  
IF EXISTS (SELECT * FROM sys.objects WHERE name = N'CleanupUnusedAssemblies')  
DROP PROCEDURE CleanupUnusedAssemblies;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE name = N'AssemblyCleanupUtils')   
DROP ASSEMBLY AssemblyCleanupUtils;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de uso y ejemplos para la integración de Common Language Runtime &#40;CLR&#41;](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
