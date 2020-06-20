---
title: Transferir datos | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- data transfers [SMO]
- transferring data
ms.assetid: eea255c3-8251-40f0-973b-fe4ef6cb5261
author: stevestein
ms.author: sstein
ms.openlocfilehash: aefe926d487a78c3ab73ac08483932e2d0a44410
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037501"
---
# <a name="transferring-data"></a>Transferir datos
  La clase <xref:Microsoft.SqlServer.Management.Smo.Transfer> es una clase de utilidad que proporciona herramientas para transferir objetos y datos.  
  
 Los objetos del esquema de la base de datos se transfieren ejecutando un script generado en el servidor de destino. Los datos de <xref:Microsoft.SqlServer.Management.Smo.Table> se transfieren con un paquete DTS creado dinámicamente.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> contiene toda la funcionalidad de los objetos <xref:Microsoft.SqlServer.Management.Smo.Transfer> de DMO y otra funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adicional. Sin embargo, en SMO en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] , el <xref:Microsoft.SqlServer.Management.Smo.Transfer> objeto usa la API [SQLBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy\(v=VS.90\).aspx) para transferir datos. Además, los métodos y propiedades que se utilizan para realizar transferencias de datos residen en el objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> en lugar del objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. Mover la funcionalidad de las clases de instancia a las clases de utilidad es coherente con un modelo de objetos más ligero porque el código para las tareas concretas solamente se carga cuando se requiere.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer> no admite transferencias de datos a una base de datos de destino cuyo valor de <xref:Microsoft.SqlServer.Management.Smo.Database.CompatibilityLevel%2A> sea menor que la versión de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-basic"></a>Transferir esquemas y datos de una base de datos a otra en Visual Basic  
 En este ejemplo de código se muestra cómo transferir esquemas y datos de una base de datos a otra utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```vb
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Create a new database that is to be destination database.
Dim dbCopy As Database
dbCopy = New Database(srv, "AdventureWorks2012Copy")
dbCopy.Create()
'Define a Transfer object and set the required options and properties.
Dim xfr As Transfer
xfr = New Transfer(db)
xfr.CopyAllTables = True
xfr.Options.WithDependencies = True
xfr.Options.ContinueScriptingOnError = True
xfr.DestinationDatabase = "AdventureWorks2012Copy"
xfr.DestinationServer = srv.Name
xfr.DestinationLoginSecure = True
xfr.CopySchema = True
'Script the transfer. Alternatively perform immediate data transfer with TransferData method.
xfr.ScriptTransfer()
```
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-visual-c"></a>Transferir esquemas y datos de una base de datos a otra en Visual C#  
 En este ejemplo de código se muestra cómo transferir esquemas y datos de una base de datos a otra utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```csharp
{  
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Create a new database that is to be destination database.   
            Database dbCopy;  
            dbCopy = new Database(srv, "AdventureWorks2012Copy");  
            dbCopy.Create();  
            //Define a Transfer object and set the required options and properties.   
            Transfer xfr;  
            xfr = new Transfer(db);  
            xfr.CopyAllTables = true;  
            xfr.Options.WithDependencies = true;  
            xfr.Options.ContinueScriptingOnError = true;  
            xfr.DestinationDatabase = "AdventureWorks2012Copy";  
            xfr.DestinationServer = srv.Name;  
            xfr.DestinationLoginSecure = true;  
            xfr.CopySchema = true;  
            //Script the transfer. Alternatively perform immediate data transfer   
            // with TransferData method.   
            xfr.ScriptTransfer();  
        }   
```  
  
## <a name="transferring-schema-and-data-from-one-database-to-another-in-powershell"></a>Transferir esquemas y datos de una base de datos a otra en PowerShell  
 En este ejemplo de código se muestra cómo transferir esquemas y datos de una base de datos a otra utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.  
  
```powershell
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Reference the AdventureWorks2012 database.  
$db = $srv.Databases["AdventureWorks2012"]  
  
#Create a database to hold the copy of AdventureWorks  
$dbCopy = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Database -ArgumentList $srv, "AdventureWorksCopy"  
$dbCopy.Create()  
  
#Define a Transfer object and set the required options and properties.  
$xfr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Transfer -ArgumentList $db  
  
#Set this objects properties  
$xfr.CopyAllTables = $true  
$xfr.Options.WithDependencies = $true  
$xfr.Options.ContinueScriptingOnError = $true  
$xfr.DestinationDatabase = "AdventureWorksCopy"  
$xfr.DestinationServer = $srv.Name  
$xfr.DestinationLoginSecure = $true  
$xfr.CopySchema = $true  
"Scripting Data Transfer"  
#Script the transfer. Alternatively perform immediate data transfer with TransferData method.  
$xfr.ScriptTransfer()  
```  
