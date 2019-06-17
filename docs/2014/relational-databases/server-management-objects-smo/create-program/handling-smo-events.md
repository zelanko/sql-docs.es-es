---
title: Controlar eventos SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- events [SMO]
- SQL Server Management Objects, events
- SMO [SQL Server], events
- events [SMO], about events
ms.assetid: b4f120dd-ba78-46ff-99c5-e47effac8544
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d0d309103880a369a88952e19b252fc15693fdd4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191923"
---
# <a name="handling-smo-events"></a>Controlar eventos SMO
  Hay tipos de evento de servidor a los que se puede suscribir utilizando un controlador de eventos y el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
 Muchas de las clases de instancia en los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO) pueden activar los eventos cuando se producen ciertas acciones en el servidor.  
  
 Estos eventos se pueden administrar mediante programación preparando un controlador de eventos y suscribiéndose a los eventos asociados. Este tipo de control de eventos es transitorio porque se quitan todas las suscripciones cuando se sale del programa cliente de SMO.  
  
## <a name="connectioncontext-event-handling"></a>Controlar eventos ConnectionContext  
 Los objetos <xref:Microsoft.SqlServer.Management.Common.ServerConnection> admiten varios tipos de evento. La propiedad del evento debe estar establecida en una instancia de un controlador de eventos adecuado y el objeto de controlador de eventos se debe definir como una función protegida que administra el evento.  
  
## <a name="event-subscription"></a>Suscripción a eventos  
 Administra los eventos escribiendo una clase de controlador de eventos, creando una instancia de él, asignando el controlador de eventos al objeto primario y suscribiéndose a continuación al evento.  
  
 Una clase de controlador de eventos se debe escribir para administrar los eventos. La clase de controlador de eventos puede contener más de una función de controlador de eventos y se debe instalar para los eventos que se van a administrar. Las funciones de controlador de eventos reciben información acerca del evento de la *ServerEventNotificatificationArgs* parámetro que puede utilizarse para presentar información sobre el evento.  
  
 Se enumeran los tipos de sucesos del servidor y la base de datos que pueden controlarse en el <xref:Microsoft.SqlServer.Management.Smo.DatabaseEventSet> clase y la <xref:Microsoft.SqlServer.Management.Smo.ServerEventSet>clase.  
  
## <a name="example"></a>Ejemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-basic"></a>Registrar los controladores de eventos y suscribirse al control de eventos en Visual Basic  
 En este ejemplo de código se muestra cómo configurar el controlador de eventos y cómo suscribirse a los eventos de base de datos.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBEvents1](SMO How to#SMO_VBEvents1)]  -->  
  
## <a name="registering-event-handlers-and-subscribing-to-event-handling-in-visual-c"></a>Registrar los controladores de eventos y suscribirse al control de eventos en Visual C#  
 En este ejemplo de código se muestra cómo configurar el controlador de eventos y cómo suscribirse a los eventos de base de datos.  
  
```  
//Create an event handler subroutine that runs when a table is created.   
private void MyCreateEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been added to the AdventureWorks2012 database.");   
}   
//Create an event handler subroutine that runs when a table is deleted.   
private void MyDropEventHandler(object sender, ServerEventArgs e)   
{   
Console.WriteLine("A table has just been dropped from the AdventureWorks2012 database.");   
}   
public void Main()   
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Create a database event set that contains the CreateTable event only.   
DatabaseEventSet databaseCreateEventSet = new DatabaseEventSet();   
databaseCreateEventSet.CreateTable = true;   
//Create a server event handler and set it to the first event handler subroutine.   
ServerEventHandler serverCreateEventHandler;   
serverCreateEventHandler = new ServerEventHandler(MyCreateEventHandler);   
//Subscribe to the first server event handler when a CreateTable event occurs.   
db.Events.SubscribeToEvents(databaseCreateEventSet, serverCreateEventHandler);   
    //Create a database event set that contains the DropTable event only.   
DatabaseEventSet databaseDropEventSet = new DatabaseEventSet();   
databaseDropEventSet.DropTable = true;   
//Create a server event handler and set it to the second event handler subroutine.   
ServerEventHandler serverDropEventHandler;   
serverDropEventHandler = new ServerEventHandler(MyDropEventHandler);   
//Subscribe to the second server event handler when a DropTable event occurs.   
db.Events.SubscribeToEvents(databaseDropEventSet, serverDropEventHandler);   
//Start event handling.   
db.Events.StartEvents();   
//Create a table on the database.   
Table tb;   
tb = new Table(db, "Test_Table");   
Column mycol1;   
mycol1 = new Column(tb, "Name", DataType.NChar(50));   
mycol1.Collation = "Latin1_General_CI_AS";   
mycol1.Nullable = true;   
tb.Columns.Add(mycol1);   
tb.Create();   
//Remove the table.   
tb.Drop();   
//Wait until the events have occured.   
int x;   
int y;   
for (x = 1; x <= 1000000000; x++) {   
    y = x * 2;   
}   
//Stop event handling.   
db.Events.StopEvents();   
}  
```  
  
  
