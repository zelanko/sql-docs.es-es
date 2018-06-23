---
title: Utilizar servidores vinculados en SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7ae91209d5786ed976e1c29ed9b51d7d52e0070a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109221"
---
# <a name="using-linked-servers-in-smo"></a>Utilizar servidores vinculados en SMO
  Un servidor vinculado representa un origen de datos OLE DB en un servidor remoto. Orígenes de datos OLE DB remotos están vinculados a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto.  
  
 Servidores de base de datos remota pueden vincularse a la instancia actual de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante un proveedor OLE DB. En SMO, los servidores vinculados están representados por la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. El <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> propiedad hace referencia a una colección de <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> objetos. Estos objetos almacenan las credenciales de inicio de sesión necesarias para establecer una conexión con el servidor vinculado.  
  
## <a name="ole-db-providers"></a>Proveedores OLE-DB  
 En SMO, una colección de objetos <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> representa los proveedores OLE DB instalados.  
  
## <a name="example"></a>Ejemplo  
 Para el siguiente ejemplo de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) y [crear a Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>Crear un vínculo a un servidor de proveedor OLE-DB en Visual Basic  
 El ejemplo de código muestra cómo crear un vínculo a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origen de datos heterogéneo mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Mediante la especificación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como el nombre del producto, acceso a los datos en el servidor vinculado mediante el uso de la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente proveedor OLE DB, que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Crear un vínculo a un servidor de proveedor OLE-DB en Visual C#  
 El ejemplo de código muestra cómo crear un vínculo a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origen de datos heterogéneo mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Mediante la especificación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como el nombre del producto, acceso a los datos en el servidor vinculado mediante el uso de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente proveedor OLE DB, que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>Crear un vínculo a un servidor de proveedor OLE-DB en PowerShell  
 El ejemplo de código muestra cómo crear un vínculo a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origen de datos heterogéneo mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Mediante la especificación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como el nombre del producto, acceso a los datos en el servidor vinculado mediante el uso de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente proveedor OLE DB, que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  