---
title: Utilizar servidores vinculados en SMO | Documentos de Microsoft
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 148be59d4e715892c3b014a29b48473b1611476e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674313"
---
# <a name="using-linked-servers-in-smo"></a>Utilizar servidores vinculados en SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Un servidor vinculado representa un origen de datos OLE DB en un servidor remoto. Orígenes de datos OLE DB remotos están vinculados a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto.  
  
 Servidores de base de datos remota se pueden vincular a la instancia actual de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante un proveedor OLE DB. En SMO, los servidores vinculados están representados por la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. El <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> propiedad hace referencia a una colección de <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> objetos. Estos objetos almacenan las credenciales de inicio de sesión necesarias para establecer una conexión con el servidor vinculado.  
  
## <a name="ole-db-providers"></a>Proveedores OLE-DB  
 En SMO, una colección de objetos <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> representa los proveedores OLE DB instalados.  
  
## <a name="example"></a>Ejemplo  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, consulte [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Crear un vínculo a un servidor de proveedor OLE-DB en Visual C#  
 El ejemplo de código muestra cómo crear un vínculo a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origen de datos heterogéneos mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Mediante la especificación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como el nombre del producto, de acceso a datos en el servidor vinculado utilizando el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente proveedor OLE DB, que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
 El ejemplo de código muestra cómo crear un vínculo a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, origen de datos heterogéneos mediante el uso de la <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto. Mediante la especificación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como el nombre del producto, de acceso a datos en el servidor vinculado utilizando el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cliente proveedor OLE DB, que es el proveedor OLE DB oficial para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
