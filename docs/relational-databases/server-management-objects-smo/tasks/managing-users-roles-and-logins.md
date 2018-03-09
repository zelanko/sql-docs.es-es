---
title: "Administrar usuarios, Roles e inicios de sesión | Documentos de Microsoft"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 47c2cf548bdc703f86a7ff90f2e32e44fceb9a7f
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="managing-users-roles-and-logins"></a>Administrar usuarios, roles e inicios de sesión
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Login> representa los inicios de sesión. Si existe un inicio de sesión en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se puede agregar a un rol del servidor. El rol de servidor representado por la <xref:Microsoft.SqlServer.Management.Smo.ServerRole> objeto. El objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> representa el rol de la base de datos y el objeto <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> representa el rol de aplicación.  
  
 Privilegios asociados con el nivel de servidor se enumeran como propiedades de la <xref:Microsoft.SqlServer.Management.Smo.ServerPermission> objeto. Los privilegios del nivel del servidor se pueden conceder, denegar o revocar de las cuentas de inicio de sesión individuales.  
  
 Cada <xref:Microsoft.SqlServer.Management.Smo.Database> objeto tiene una <xref:Microsoft.SqlServer.Management.Smo.UserCollection> objeto que especifica todos los usuarios en la base de datos. Cada usuario está asociado a un inicio de sesión. Se puede asociar un inicio de sesión con usuarios en más de una base de datos. El <xref:Microsoft.SqlServer.Management.Smo.Login> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> método se puede utilizar para enumerar todos los usuarios en cada base de datos que está asociado con el inicio de sesión. Alternativamente, la propiedad <xref:Microsoft.SqlServer.Management.Smo.User> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> especifica el inicio de sesión asociado con el usuario.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]bases de datos también tienen roles que especifican un conjunto de privilegios de nivel de base de datos que permiten a un usuario realizar tareas específicas. A diferencia de los roles del servidor, los roles de la base de datos no son fijos. Se pueden crear, modificar y quitar. Los privilegios y usuarios pueden estar asignados a un rol de la base de datos para la administración masiva.  
  
## <a name="example"></a>Ejemplo  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear a Visual C &#35; Proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>Enumerar inicios de sesión y usuarios asociados en Visual C#  
 Cada usuario de una base de datos está asociado a un inicio de sesión. El inicio de sesión puede asociarse a usuarios de más de una base de datos. El ejemplo de código muestra cómo llamar al método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para hacer una lista de todos los usuarios de la base de datos que están asociados al inicio de sesión. En el ejemplo se crea un inicio de sesión y un usuario en el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos para asegurarse de que no hay información de asignación que enumerar.  
  
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
 Cada usuario de una base de datos está asociado a un inicio de sesión. El inicio de sesión puede asociarse a usuarios de más de una base de datos. El ejemplo de código muestra cómo llamar al método <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Login> para hacer una lista de todos los usuarios de la base de datos que están asociados al inicio de sesión. En el ejemplo se crea un inicio de sesión y un usuario en el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos para asegurarse de que no hay información de asignación que enumerar.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\Default\Databases  
  
#Iterate through all databases  
 foreach ($db in Get-ChildItem)  
 {  
 "====="  
 "Login Mappings for the database: "+ $db.Name  
  
 #get the datatable containing the mapping from the smo database oject  
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
 Este ejemplo muestra cómo administrar los roles y los usuarios. Para ejecutar este ejemplo debe hacer referencia a los ensamblados siguientes:  
  
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
  
  
