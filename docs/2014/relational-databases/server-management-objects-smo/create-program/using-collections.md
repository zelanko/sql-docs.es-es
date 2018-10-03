---
title: Uso de colecciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33c0d43f3be1ca48904a7e4fa130f04ea0cc7445
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174985"
---
# <a name="using-collections"></a>Usar colecciones
  Una colección es una lista de objetos construidos desde la misma clase de objeto y que comparten el mismo objeto primario. El objeto de colección contiene siempre el nombre del tipo de objeto con el sufijo Collection. Por ejemplo, para tener acceso a las columnas de una tabla determinada, use el tipo de objeto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Contiene todos los objetos <xref:Microsoft.SqlServer.Management.Smo.Column> que pertenecen al mismo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each` instrucción o el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach` instrucción puede usarse para iterar por cada miembro de la colección.  
  
## <a name="examples"></a>Ejemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Hacer referencia a un objeto mediante una colección en Visual Basic  
 Este ejemplo de código muestra cómo establecer una propiedad de columna mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>, y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> propiedades. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> propiedad del objeto de colección.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Hacer referencia a un objeto mediante una colección en Visual C#  
 Este ejemplo de código muestra cómo establecer una propiedad de columna mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>, y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> propiedades. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> propiedad del objeto de colección.  
  
```  
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
 Este ejemplo de código se recorre el <xref:Microsoft.AnalysisServices.Server.Databases%2A> propiedad de colección y se muestran todas las conexiones a la instancia de la base de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Recorrer en iteración los miembros de una colección en Visual C#  
 Este ejemplo de código se recorre el <xref:Microsoft.AnalysisServices.Server.Databases%2A> propiedad de colección y se muestran todas las conexiones a la instancia de la base de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
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
  
  
