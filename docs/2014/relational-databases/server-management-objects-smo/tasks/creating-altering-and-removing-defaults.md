---
title: Crear, modificar y quitar valores predeterminados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- defaults [SMO]
ms.assetid: c30ac3b9-8150-4264-ba4c-c549f44261ab
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dcc29aa897674ae61d6bc5e8a53abe109661ebbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797157"
---
# <a name="creating-altering-and-removing-defaults"></a>Crear, modificar y eliminar valores predeterminados
  En los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO), el objeto <xref:Microsoft.SqlServer.Management.Smo.Default> representa la restricción predeterminada.  
  
 La propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Default> se utiliza para definir el valor que se insertará. Puede ser una constante o una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] que devuelve un valor constante, como GETDATE(). La propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> no puede modificarse mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. En lugar de ello, debe quitarse el objeto <xref:Microsoft.SqlServer.Management.Smo.Default> y volver a crearse.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual Basic SMO en Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-default-in-visual-basic"></a>Crear, modificar y quitar un valor predeterminado en Visual Basic  
 En este ejemplo de código se muestra cómo crear un valor predeterminado que está formado por texto simple y otro valor predeterminado que es una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] . El valor predeterminado debe adjuntarse a la columna mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> y desasociarse utilizando el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDefaults1](SMO How to#SMO_VBDefaults1)]  -->  
  
## <a name="creating-altering-and-removing-a-default-in-visual-c"></a>Crear, modificar y quitar un valor predeterminado en Visual C#  
 En este ejemplo de código se muestra cómo crear un valor predeterminado que está formado por texto simple y otro valor predeterminado que es una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] . El valor predeterminado debe adjuntarse a la columna mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> y desasociarse utilizando el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
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
 En este ejemplo de código se muestra cómo crear un valor predeterminado que está formado por texto simple y otro valor predeterminado que es una instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] . El valor predeterminado debe adjuntarse a la columna mediante el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.BindToColumn%2A> y desasociarse utilizando el método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.UnbindFromColumn%2A>.  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
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
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.SqlServer.Management.Smo.Default>  
