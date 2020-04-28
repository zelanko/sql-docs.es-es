---
title: Usar servidores vinculados en SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f62efaa1550ea0b9e68ce4914e4852612d53f48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72781994"
---
# <a name="using-linked-servers-in-smo"></a>Utilizar servidores vinculados en SMO
  Un servidor vinculado representa un origen de datos OLE DB en un servidor remoto. Los orígenes de datos OLE DB remotos están vinculados a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la utilización del objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>.  
  
 Los servidores de bases de datos remotos se pueden vincular a la instancia actual de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante un proveedor de OLE DB. EN SMO, los servidores vinculados están representados por el objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. La propiedad <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> hace referencia a una colección de objetos <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>. Estos objetos almacenan las credenciales de inicio de sesión necesarias para establecer una conexión con el servidor vinculado.  
  
## <a name="ole-db-providers"></a>Proveedores OLE-DB  
 En SMO, una colección de objetos <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> representa los proveedores OLE DB instalados.  
  
## <a name="example"></a>Ejemplo  
 Para el siguiente ejemplo de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual Basic SMO en Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) y [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-basic"></a>Crear un vínculo a un servidor de proveedor OLE-DB en Visual Basic  
 En el ejemplo de código se muestra cómo crear un vínculo a un origen de datos heterogéneo OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Al especificar como el nombre del producto, se obtiene acceso a los datos en el servidor vinculado [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el proveedor de OLE DB del cliente, que es el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]proveedor de OLE DB oficial para.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLinkedServers1](SMO How to#SMO_VBLinkedServers1)]  -->  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Crear un vínculo a un servidor de proveedor OLE-DB en Visual C#  
 En el ejemplo de código se muestra cómo crear un vínculo a un origen de datos heterogéneo OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Especificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como nombre de producto, se obtiene acceso a los datos en el servidor vinculado utilizando el proveedor OLE DB de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp
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
 En el ejemplo de código se muestra cómo crear un vínculo a un origen de datos heterogéneo OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>. Especificando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como nombre de producto, se obtiene acceso a los datos en el servidor vinculado utilizando el proveedor OLE DB de cliente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```powershell
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -ArgumentList $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.
$lsvr.ProductName = "SQL Server"
  
#Create the Database Object  
$lsvr.Create()
```  
