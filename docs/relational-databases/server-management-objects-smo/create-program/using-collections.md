---
title: Uso de colecciones | Documentos de Microsoft
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
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac05072224f6b6cc4e84b2144d827b6059b226d2
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="using-collections"></a>Usar colecciones
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Una colección es una lista de objetos construidos desde la misma clase de objeto y que comparten el mismo objeto primario. El objeto de colección contiene siempre el nombre del tipo de objeto con el sufijo Collection. Por ejemplo, para tener acceso a las columnas de una tabla determinada, use el tipo de objeto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Contiene todos los objetos <xref:Microsoft.SqlServer.Management.Smo.Column> que pertenecen al mismo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] **para... Cada** instrucción o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] **foreach** instrucción puede utilizarse para recorrer en iteración todos los miembros de la colección.  
  
## <a name="examples"></a>Ejemplos  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear a Visual C &#35; Proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Hacer referencia a un objeto mediante una colección en Visual Basic  
 Este ejemplo de código muestra cómo establecer una propiedad de columna mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>, y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> propiedades. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> propiedad del objeto de colección.  
  
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
 Este ejemplo de código muestra cómo establecer una propiedad de columna mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>, y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> propiedades. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> propiedad del objeto de colección.  
  
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
 Este ejemplo de código recorre en iteración la <xref:Microsoft.AnalysisServices.Server.Databases%2A> propiedad de colección y se muestran todas las conexiones a la instancia de la base de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
 Este ejemplo de código recorre en iteración la <xref:Microsoft.AnalysisServices.Server.Databases%2A> propiedad de colección y se muestran todas las conexiones a la instancia de la base de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
  
  
