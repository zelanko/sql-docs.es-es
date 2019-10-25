---
title: Crear, modificar y eliminar bases de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- databases [SMO]
- databases [SMO], creating
- databases [SMO], modifying
- databases [SMO], deleting
ms.assetid: fcfb3ec2-7556-4f72-971a-501295892cb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 645ba8428dddb36de9a3edeb784d64f96b5c0603
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797041"
---
# <a name="creating-altering-and-removing-databases"></a>Crear, modificar y eliminar bases de datos
  El objeto <xref:Microsoft.SqlServer.Management.Smo.Database> representa una base de datos en SMO.  
  
 Para crear un objeto <xref:Microsoft.SqlServer.Management.Smo.Database> no es necesario modificarlo o quitarlo. Se puede hacer referencia a la base de datos utilizando una recopilación.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual Basic SMO en Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un&#35; proyecto de Visual C SMO en Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-database-in-visual-basic"></a>Crear, modificar y quitar una base de datos en Visual Basic  
 En este ejemplo de código se crea una nueva base de datos. Automáticamente, se crean archivos y grupos de archivos para la base de datos.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDatabase1](SMO How to#SMO_VBDatabase1)]  -->  
  
## <a name="creating-altering-and-removing-a-database-in-visual-c"></a>Crear, modificar y quitar una base de datos en Visual C#  
 En este ejemplo de código se crea una nueva base de datos. Automáticamente, se crean archivos y grupos de archivos para la base de datos.  
  
```csharp
{  
                //Connect to the local, default instance of SQL Server.   
                Server srv;  
                srv = new Server();  
                //Define a Database object variable by supplying the server and the database name arguments in the constructor.   
                Database db;  
                db = new Database(srv, "Test_SMO_Database");  
                //Create the database on the instance of SQL Server.   
                db.Create();  
                //Reference the database and display the date when it was created.   
                db = srv.Databases["Test_SMO_Database"];  
                Console.WriteLine(db.CreateDate);  
                //Remove the database.   
                db.Drop();  
            }  
```  
  
## <a name="creating-altering-and-removing-a-database-in-powershell"></a>Crear, modificar y quitar una base de datos en PowerShell  
 En este ejemplo de código se crea una nueva base de datos. Automáticamente, se crean archivos y grupos de archivos para la base de datos.  
  
```powershell
#Get a server object which corresponds to the default instance  
cd \sql\localhost\  
$srv = Get-Item default  
  
#Create a new database  
$db = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Database -argumentlist $srv, "Test_SMO_Database"  
$db.Create()  
  
#Reference the database and display the date when it was created.
$db = $srv.Databases["Test_SMO_Database"]  
$db.CreateDate  
  
#Drop the database  
$db.Drop()  
```  
  
## <a name="see-also"></a>Ver también  
 <xref:Microsoft.SqlServer.Management.Smo.Database>  
