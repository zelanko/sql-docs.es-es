---
description: Crear, modificar y quitar reglas
title: Crear, modificar y quitar reglas
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3fcf4dca6ec2cc56ddab8a847afd87c96811e96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420249"
---
# <a name="creating-altering-and-removing-rules"></a>Crear, modificar y quitar reglas
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  En SMO, el objeto <xref:Microsoft.SqlServer.Management.Smo.Rule> representa las reglas. La propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A>, que es una cadena de texto que contiene una expresión de condición que utiliza operadores o predicados, como IN, LIKE o BETWEEN, define la regla. Una regla no puede hacer referencia a columnas u otros objetos de base de datos. Se pueden incluir funciones integradas que no hagan referencia a objetos de base de datos.  
  
 La definición en la propiedad <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> debe contener una variable que haga referencia al valor de datos escrito. Se puede utilizar cualquier nombre o símbolo para representar el valor cuando se crea la regla, pero el primer carácter debe ser el \@ símbolo.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>Crear, modificar y quitar una regla en Visual Basic  
 En este ejemplo de código se muestra cómo crear una regla, cómo adjuntarla a una columna, cómo modificar las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, cómo desasociar la regla de la columna y, por último, cómo quitarla.  
  
 La instrucción **Dim** del <xref:Microsoft.SqlServer.Management.Smo.Rule> objeto se especifica con la ruta de acceso completa del ensamblado para evitar la ambigüedad con un <xref:Microsoft.SqlServer.Management.Smo.Rule> objeto en el ensamblado System. Data.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>Crear, modificar y quitar una regla en Visual C#  
 En este ejemplo de código se muestra cómo crear una regla, cómo adjuntarla a una columna, cómo modificar las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Rule>, cómo desasociar la regla de la columna y, por último, cómo quitarla.  
  
 La instrucción **Dim** del <xref:Microsoft.SqlServer.Management.Smo.Rule> objeto se especifica con la ruta de acceso completa del ensamblado para evitar la ambigüedad con un <xref:Microsoft.SqlServer.Management.Smo.Rule> objeto en el ensamblado System. Data.  
  
```csharp  
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
  
 La instrucción **Dim** del <xref:Microsoft.SqlServer.Management.Smo.Rule> objeto se especifica con la ruta de acceso completa del ensamblado para evitar la ambigüedad con un <xref:Microsoft.SqlServer.Management.Smo.Rule> objeto en el ensamblado System. Data.  
  
```powershell   
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
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
