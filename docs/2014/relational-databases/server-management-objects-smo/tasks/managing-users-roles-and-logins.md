---
title: Administración de usuarios, roles e inicios de sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86b67202537e650619f835e9c64d2c35a8e78fc2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72796605"
---
# <a name="managing-users-roles-and-logins"></a>Administrar usuarios, roles e inicios de sesión
  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Login> representa los inicios de sesión. Si existe un inicio de sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se puede agregar a un rol del servidor. El objeto <xref:Microsoft.SqlServer.Management.Smo.ServerRole> representa el rol del servidor. El objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> representa el rol de la base de datos y el objeto <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> representa el rol de aplicación.  
  
 Los privilegios asociados al nivel del servidor se enumeran como propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>. Los privilegios del nivel del servidor se pueden conceder, denegar o revocar de las cuentas de inicio de sesión individuales.  
  
 Cada objeto <xref:Microsoft.SqlServer.Management.Smo.Database> tiene un objeto <xref:Microsoft.SqlServer.Management.Smo.UserCollection> que especifica todos los usuarios en la base de datos. Cada usuario está asociado a un inicio de sesión. Se puede asociar un inicio de sesión con usuarios en más de una base de datos. El método <xref:Microsoft.SqlServer.Management.Smo.Login> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> se puede utilizar para hacer una lista de todos los usuarios en cada base de datos que está asociada al inicio de sesión. Alternativamente, la propiedad <xref:Microsoft.SqlServer.Management.Smo.User> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> especifica el inicio de sesión asociado con el usuario.  
  
 Las bases de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] también tienen roles que especifican un conjunto de privilegios en el nivel de base de datos que permiten a un usuario realizar tareas concretas. A diferencia de los roles del servidor, los roles de la base de datos no son fijos. Se pueden crear, modificar y quitar. Los privilegios y usuarios pueden estar asignados a un rol de la base de datos para la administración masiva.  
  
## <a name="example"></a>Ejemplo  
 Para el siguiente ejemplo de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual Basic SMO en Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) y [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="enumerating-logins-and-associated-users-in-visual-basic"></a>Enumerar inicios de sesión y usuarios asociados en Visual Basic  
 Cada usuario de una base de datos está asociado a un inicio de sesión. El inicio de sesión puede asociarse a usuarios de más de una base de datos. El ejemplo de código muestra cómo llamar al método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para hacer una lista de todos los usuarios de la base de datos que están asociados al inicio de sesión. En el ejemplo se crean un inicio de sesión y un usuario en la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] para asegurarse de que hay información de asignación que mostrar.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLogins1](SMO How to#SMO_VBLogins1)]  -->  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>Enumerar inicios de sesión y usuarios asociados en Visual C#  
 Cada usuario de una base de datos está asociado a un inicio de sesión. El inicio de sesión puede asociarse a usuarios de más de una base de datos. El ejemplo de código muestra cómo llamar al método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para hacer una lista de todos los usuarios de la base de datos que están asociados al inicio de sesión. En el ejemplo se crean un inicio de sesión y un usuario en la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] para asegurarse de que hay información de asignación que mostrar.  
  
```csharp
{   
Server srv = new Server();   
//Iterate through each database and display.   
  
foreach ( Database db in srv.Databases) {   
   Console.WriteLine("========");   
   Console.WriteLine("Login Mappings for the database: " + db.Name);   
   Console.WriteLine(" ");   
   //Run the EnumLoginMappings method and return details of database user-login mappings to a DataTable object variable.   
   DataTable d;  
   d = db.EnumLoginMappings();   
   //Display the mapping information.   
   foreach (DataRow r in d.Rows) {   
      foreach (DataColumn c in r.Table.Columns) {   
         Console.WriteLine(c.ColumnName + " = " + r[c]);   
      }   
      Console.WriteLine(" ");   
   }   
}   
}  
```  
  
## <a name="enumerating-logins-and-associated-users-in-powershell"></a>Enumerar inicios de sesión y usuarios asociados en PowerShell  
 Cada usuario de una base de datos está asociado a un inicio de sesión. El inicio de sesión puede asociarse a usuarios de más de una base de datos. El ejemplo de código muestra cómo llamar al método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para hacer una lista de todos los usuarios de la base de datos que están asociados al inicio de sesión. En el ejemplo se crean un inicio de sesión y un usuario en la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] para asegurarse de que hay información de asignación que mostrar.  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\Default\Databases  
  
#Iterate through all databases  
 foreach ($db in Get-ChildItem)  
 {  
 "====="  
 "Login Mappings for the database: "+ $db.Name  
  
 #get the datatable containing the mapping from the smo database object  
 $dt = $db.EnumLoginMappings()  
  
 #display the results  
 foreach($row in $dt.Rows)  
     {  
        foreach($col in $row.Table.Columns)  
      {  
        $col.ColumnName + "=" + $row[$col]  
       }
     }  
 }  
```  
  
## <a name="managing-roles-and-users"></a>Administrar roles y usuarios  
 Este ejemplo muestra cómo administrar los roles y los usuarios. En el primer ejemplo se usa C# y en el segundo Visual Basic. Los siguientes ejemplos de código requieren una referencia a los siguientes ensamblados:  
  
-   Microsoft.SqlServer.Smo.dll  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
-   Microsoft.SqlServer.ConnectionInfo.dll  
  
-   Microsoft.SqlServer.SqlEnum.dll  
  
```csharp
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // Creating Logins  
      Login login = new Login(svr, "Login1");  
      login.LoginType = LoginType.SqlLogin;  
      login.Create("password@1");  
  
      Login login2 = new Login(svr, "Login2");  
      login2.LoginType = LoginType.SqlLogin;  
      login2.Create("password@1");  
  
      // Creating Users in the database for the logins created  
      User user1 = new User(db, "User1");  
      user1.Login = "Login1";  
      user1.Create();  
  
      User user2 = new User(db, "User2");  
      user2.Login = "Login2";  
      user2.Create();  
  
      // Creating database permission Sets  
      DatabasePermissionSet dbPermSet = new DatabasePermissionSet(DatabasePermission.AlterAnySchema);  
      dbPermSet.Add(DatabasePermission.AlterAnyUser);  
  
      DatabasePermissionSet dbPermSet2 = new DatabasePermissionSet(DatabasePermission.CreateType);  
      dbPermSet2.Add(DatabasePermission.CreateSchema);  
      dbPermSet2.Add(DatabasePermission.CreateTable);  
  
      // Creating Database roles  
      DatabaseRole role1 = new DatabaseRole(db, "Role1");  
      role1.Create();  
  
      DatabaseRole role2 = new DatabaseRole(db, "Role2");  
      role2.Create();  
  
      // Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name);  
      db.Grant(dbPermSet2, role2.Name);  
  
      // Adding members (Users / Roles) to Role  
      role1.AddMember("User1");  
  
      role2.AddMember("User2");  
  
      // Role1 becomes a member of Role2  
      role2.AddMember("Role1");  
  
      // Enumerating through explicit permissions granted to Role1  
      // enumerates all database permissions for the Grantee  
      DatabasePermissionInfo[] dbPermsRole1 = db.EnumDatabasePermissions("Role1");     
      foreach (DatabasePermissionInfo dbp in dbPermsRole1) {  
         Console.WriteLine(dbp.Grantee + " has " + dbp.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
   }  
}  
```  
  
 Esta es la versión de Visual Basic:  
  
```vb
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
   Public Shared Sub Main()  
      Dim svr As New Server()  
      Dim db As New Database(svr, "TESTDB")  
      db.Create()  
  
      ' Creating Logins  
      Dim login As New Login(svr, "Login1")  
      login.LoginType = LoginType.SqlLogin  
      login.Create("password@1")  
  
      Dim login2 As New Login(svr, "Login2")  
      login2.LoginType = LoginType.SqlLogin  
      login2.Create("password@1")  
  
      ' Creating Users in the database for the logins created  
      Dim user1 As New User(db, "User1")  
      user1.Login = "Login1"  
      user1.Create()  
  
      Dim user2 As New User(db, "User2")  
      user2.Login = "Login2"  
      user2.Create()  
  
      ' Creating database permission Sets  
      Dim dbPermSet As New DatabasePermissionSet(DatabasePermission.AlterAnySchema)  
      dbPermSet.Add(DatabasePermission.AlterAnyUser)  
  
      Dim dbPermSet2 As New DatabasePermissionSet(DatabasePermission.CreateType)  
      dbPermSet2.Add(DatabasePermission.CreateSchema)  
      dbPermSet2.Add(DatabasePermission.CreateTable)  
  
      ' Creating Database roles  
      Dim role1 As New DatabaseRole(db, "Role1")  
      role1.Create()  
  
      Dim role2 As New DatabaseRole(db, "Role2")  
      role2.Create()  
  
      ' Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name)  
      db.Grant(dbPermSet2, role2.Name)  
  
      ' Adding members (Users / Roles) to Role  
      role1.AddMember("User1")  
  
      role2.AddMember("User2")  
  
      ' Role1 becomes a member of Role2  
      role2.AddMember("Role1")  
  
      ' Enumerating through explicit permissions granted to Role1  
      ' enumerates all database permissions for the Grantee  
      Dim dbPermsRole1 As DatabasePermissionInfo() = db.EnumDatabasePermissions("Role1")  
      For Each dbp As DatabasePermissionInfo In dbPermsRole1  
         Console.WriteLine(dbp.Grantee + " has " & dbp.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine(" ")  
   End Sub  
End Class  
```  
