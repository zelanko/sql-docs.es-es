---
title: Uso de colecciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
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
ms.openlocfilehash: 0be31e67be0b80de13a9239b221ca73436a8d6e7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813927"
---
# <a name="using-collections"></a>Usar colecciones
  Una colección es una lista de objetos construidos desde la misma clase de objeto y que comparten el mismo objeto primario. El objeto de colección contiene siempre el nombre del tipo de objeto con el sufijo Collection. Por ejemplo, para tener acceso a las columnas de una tabla determinada, use el tipo de objeto <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection>. Contiene todos los objetos <xref:Microsoft.SqlServer.Management.Smo.Column> que pertenecen al mismo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.  
  
 El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each` instrucción o el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach` instrucción puede usarse para iterar por cada miembro de la colección.  
  
## <a name="examples"></a>Ejemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>Hacer referencia a un objeto mediante una colección en Visual Basic  
 En este ejemplo de código se muestra cómo establecer una propiedad de columna mediante las propiedades <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la propiedad de objeto de colección <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>Hacer referencia a un objeto mediante una colección en Visual C#  
 En este ejemplo de código se muestra cómo establecer una propiedad de columna mediante las propiedades <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>, <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> y <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>. Estas propiedades representan colecciones que se pueden usar para identificar un objeto determinado cuando se usan con un parámetro que especifica el nombre del objeto. El nombre y el esquema son necesarios para la propiedad de objeto de colección <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>.  
  
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
 En este ejemplo de código se recorre en iteración la propiedad de colección <xref:Microsoft.AnalysisServices.Server.Databases%2A> y se muestran todas las conexiones a bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>Recorrer en iteración los miembros de una colección en Visual C#  
 En este ejemplo de código se recorre en iteración la propiedad de colección <xref:Microsoft.AnalysisServices.Server.Databases%2A> y se muestran todas las conexiones a bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
  
  
