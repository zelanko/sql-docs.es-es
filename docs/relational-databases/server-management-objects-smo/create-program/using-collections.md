---
title: Usar colecciones | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c3f4c31da84c2ca07b948faeba4aed7b93ad011
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70148693"
---
# <a name="using-collections"></a>Usar colecciones
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Una colección es una lista de objetos construidos desde la misma clase de objeto y que comparten el mismo objeto primario. El objeto de colección contiene siempre el nombre del tipo de objeto con el sufijo Collection. Por ejemplo, para tener acceso a las columnas de una tabla determinada, use el tipo de objeto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Contiene todos los objetos <xref:Microsoft.SqlServer.Management.Smo.Column> que pertenecen al mismo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 La instrucción [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] **vbprvb** o la instrucción [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] **csprcs** pueden usarse para recorrer en iteración todos los miembros de la colección.  
  
## <a name="examples"></a>Ejemplos  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Hacer referencia a un objeto mediante una colección en Visual Basic  
 En este ejemplo de código se muestra cómo establecer una propiedad de columna mediante las propiedades <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la propiedad de objeto de colección <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Modify a property using the Databases, Tables, and Columns collections to reference a column.
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("ModifiedDate").Nullable = True
'Call the Alter method to make the change on the instance of SQL Server.
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("ModifiedDate").Alter()
```
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Hacer referencia a un objeto mediante una colección en Visual C#  
 En este ejemplo de código se muestra cómo establecer una propiedad de columna mediante las propiedades <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la propiedad de objeto de colección <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>Recorrer en iteración los miembros de una colección en Visual Basic  
 En este ejemplo de código se recorre en iteración la propiedad de colección <xref:Microsoft.AnalysisServices.Server.Databases%2A> y se muestran todas las conexiones a bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
Dim count As Integer
Dim total As Integer
'Iterate through the databases and call the GetActiveDBConnectionCount method.
Dim db As Database
For Each db In srv.Databases
    count = srv.GetActiveDBConnectionCount(db.Name)
    total = total + count
    'Display the number of connections for each database.
    Console.WriteLine(count & " connections on " & db.Name)
Next
'Display the total number of connections on the instance of SQL Server.
Console.WriteLine("Total connections =" & total)
```
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Recorrer en iteración los miembros de una colección en Visual C#  
 En este ejemplo de código se recorre en iteración la propiedad de colección <xref:Microsoft.AnalysisServices.Server.Databases%2A> y se muestran todas las conexiones a bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
