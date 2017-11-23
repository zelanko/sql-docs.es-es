---
title: Crear, modificar y eliminar valores predeterminados | Documentos de Microsoft
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e79fad6e2c3e241c665a6869695e56aaed4d9158
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="creating-altering-and-removing-defaults"></a>Crear, modificar y eliminar valores predeterminados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), la restricción predeterminada está representada por la <xref:Microsoft.SqlServer.Management.Smo.Default> objeto.  
  
 La propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Default> se utiliza para definir el valor que se insertará. Puede ser una constante o una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] que devuelve un valor constante, como GETDATE(). La propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> no puede modificarse mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. En lugar de ello, debe quitarse el objeto <xref:Microsoft.SqlServer.Management.Smo.Default> y volver a crearse.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear a Visual C &#35; Proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Crear, modificar y quitar un valor predeterminado en Visual Basic  
 En este ejemplo de código se muestra cómo crear un valor predeterminado que está formado por texto simple y otro valor predeterminado que es una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El valor predeterminado debe adjuntarse a la columna mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> y desasociarse utilizando el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Default object variable by supplying the parent database and the default name 
'in the constructor.
Dim def As [Default]
def = New [Default](db, "Test_Default2")
'Set the TextHeader and TextBody properties that define the default.
def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"
def.TextBody = "GetDate()"
'Create the default on the instance of SQL Server.
def.Create()
'Declare a Column object variable and reference a column in the AdventureWorks2012 database.
Dim col As Column
col = db.Tables("SpecialOffer", "Sales").Columns("StartDate")
'Bind the default to the column.
def.BindToColumn("SpecialOffer", "StartDate", "Sales")
'Unbind the default from the column and remove it from the database.
def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")
def.Drop()
```
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Crear, modificar y quitar un valor predeterminado en Visual C#  
 En este ejemplo de código se muestra cómo crear un valor predeterminado que está formado por texto simple y otro valor predeterminado que es una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El valor predeterminado debe adjuntarse a la columna mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> y desasociarse utilizando el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```csharp  
{  
  
          Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database  db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Default object variable by supplying the parent database and the default name   
            //in the constructor.   
            Default def = new Default(db, "Test_Default2");  
  
            //Set the TextHeader and TextBody properties that define the default.   
            def.TextHeader = "CREATE DEFAULT [Test_Default2] AS";  
            def.TextBody = "GetDate()";  
  
            //Create the default on the instance of SQL Server.   
            def.Create();  
  
            //Bind the default to a column in a table in AdventureWorks2012  
            def.BindToColumn("SpecialOffer", "StartDate", "Sales");  
  
            //Unbind the default from the column and remove it from the database.   
            def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales");  
            def.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-default-in-powershell"></a>Crear, modificar y quitar un valor predeterminado en PowerShell  
 En este ejemplo de código se muestra cómo crear un valor predeterminado que está formado por texto simple y otro valor predeterminado que es una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El valor predeterminado debe adjuntarse a la columna mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> y desasociarse utilizando el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
#Define a Default object variable by supplying the parent database and the default name in the constructor.  
$def = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Default `  
-argumentlist $db, "Test_Default2"  
  
#Set the TextHeader and TextBody properties that define the default.   
$def.TextHeader = "CREATE DEFAULT [Test_Default2] AS"  
$def.TextBody = "GetDate()"  
  
#Create the default on the instance of SQL Server.   
$def.Create()  
  
#Bind the default to the column.   
$def.BindToColumn("SpecialOffer", "StartDate", "Sales")  
  
#Unbind the default from the column and remove it from the database.   
$def.UnbindFromColumn("SpecialOffer", "StartDate", "Sales")  
$def.Drop()  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
  
  
