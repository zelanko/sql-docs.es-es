---
title: Crear, modificar y quitar reglas | Documentos de Microsoft
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
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1e3b9022911f69576cead7c44283fcad362d57c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106526"
---
# <a name="creating-altering-and-removing-rules"></a>Crear, modificar y quitar reglas
  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> representa las reglas. La propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A>, que es una cadena de texto que contiene una expresión de condición que utiliza operadores o predicados, como IN, LIKE o BETWEEN, define la regla. Una regla no puede hacer referencia a columnas u otros objetos de base de datos. Se pueden incluir funciones integradas que no hagan referencia a objetos de base de datos.  
  
 La definición en la propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> debe contener una variable que haga referencia al valor de datos escrito. Se puede utilizar cualquier nombre o símbolo para representar el valor cuando se crea la regla, pero el primer carácter debe ser la arroba (@).  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear a Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Crear, modificar y quitar una regla en Visual Basic  
 En este ejemplo de código se muestra cómo crear una regla, cómo adjuntarla a una columna, cómo modificar las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, cómo desasociar la regla de la columna y, por último, cómo quitarla.  
  
 La instrucción `Dim` para el objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> se especifica con la ruta completa del ensamblado para evitar la ambigüedad con un objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> en el ensamblado System.Data.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBRules1](SMO How to#SMO_VBRules1)]  -->  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Crear, modificar y quitar una regla en Visual C#  
 En este ejemplo de código se muestra cómo crear una regla, cómo adjuntarla a una columna, cómo modificar las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, cómo desasociar la regla de la columna y, por último, cómo quitarla.  
  
 La instrucción `Dim` para el objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> se especifica con la ruta completa del ensamblado para evitar la ambigüedad con un objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> en el ensamblado System.Data.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>Crear, modificar y quitar una regla en PowerShell  
 En este ejemplo de código se muestra cómo crear una regla, cómo adjuntarla a una columna, cómo modificar las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, cómo desasociar la regla de la columna y, por último, cómo quitarla.  
  
 La instrucción `Dim` para el objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> se especifica con la ruta completa del ensamblado para evitar la ambigüedad con un objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> en el ensamblado System.Data.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  