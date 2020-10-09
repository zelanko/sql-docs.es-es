---
description: Desconectar de una instancia de SQL Server
title: Desconectar de una instancia de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e98180b877fb81c5d32f908a2f8e9cdc131a45a
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868611"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectar de una instancia de SQL Server
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  No se requiere cerrar ni desconectar manualmente los objetos de Objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO). Las conexiones se abren y se cierra según se requiere.  
  
## <a name="connection-pooling"></a>Agrupar conexiones  
 Cuando se llama al método [Connect](/previous-versions/sql/sql-server-2014/ms199449(v=sql.120)) , la conexión no se libera automáticamente. Se debe llamar al método [Disconnect](/previous-versions/sql/sql-server-2014/ms199428(v=sql.120)) explícitamente para liberar la conexión al grupo de conexiones. También puede solicitar una conexión no agrupada. Para ello, establezca la propiedad [NonPooledConnection](/previous-versions/sql/sql-server-2014/ms214357(v=sql.120)) de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad que hace referencia al objeto [ServerConnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120)) .  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectar de una instancia de SQL Server para RMO  
 El cierre de las conexiones de servidor cuando se programa con RMO funciona de forma ligeramente diferente a SMO.  
  
 Dado que el objeto [ServerConnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120)) mantiene la conexión de servidor para un objeto RMO, este objeto también se usa al desconectar de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando se programa con RMO. Para cerrar una conexión mediante el objeto [ServerConnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120)) , llame al método [Disconnect](/previous-versions/sql/sql-server-2014/ms199428(v=sql.120)) del objeto RMO. Una vez cerrada la conexión, no se pueden utilizar objetos RMO.  
  
## <a name="example"></a>Ejemplo  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Cerrar y desconectar un objeto SMO en Visual Basic  
 En este ejemplo de código se muestra cómo solicitar una conexión no agrupada estableciendo la propiedad [NonPooledConnection](/previous-versions/sql/sql-server-2014/ms214357(v=sql.120)) de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad de objeto.  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Cerrar y desconectar un objeto SMO en Visual C#  
 En este ejemplo de código se muestra cómo solicitar una conexión no agrupada estableciendo la propiedad [NonPooledConnection](/previous-versions/sql/sql-server-2014/ms214357(v=sql.120)) de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad de objeto.  
  
```csharp  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120))  
  
