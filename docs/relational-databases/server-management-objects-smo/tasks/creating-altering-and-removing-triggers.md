---
title: Crear, modificar y quitar desencadenadores | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
caps.latest.revision: 48
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9ce8e01f603bb7ec2fde42b36af186b9a03b1994
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38018449"
---
# <a name="creating-altering-and-removing-triggers"></a>Crear, modificar y eliminar desencadenadores
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  En SMO, los desencadenadores se representan utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>. El [!INCLUDE[tsql](../../../includes/tsql-md.md)] código que se ejecuta cuando se establece el desencadenador que se desencadena la <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> propiedad del objeto desencadenador. El tipo de desencadenador se establece utilizando otras propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>, como la propiedad <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A>. Se trata de una propiedad booleana que especifica si el desencadenador se activa por una **UPDATE** de los registros en la tabla primaria.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger> representa los desencadenadores tradicionales del lenguaje de manipulación de datos (DML). En [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y en versiones posteriores, también se admiten los desencadenadores del lenguaje de definición de datos (DDL). El objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> y el objeto <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger> representan los desencadenadores DDL.  
  
## <a name="example"></a>Ejemplo  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>Crear, modificar y quitar un desencadenador en Visual Basic  
 En este ejemplo de código se muestra cómo crear e insertar un desencadenador de actualización en una tabla existente, denominada `Sales`, en la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. El desencadenador envía un mensaje de aviso cuando la tabla se actualiza o cuando se inserta un nuevo registro.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>Crear, modificar y quitar un desencadenador en Visual C#  
 En este ejemplo de código se muestra cómo crear e insertar un desencadenador de actualización en una tabla existente, denominada `Sales`, en la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. El desencadenador envía un mensaje de aviso cuando la tabla se actualiza o cuando se inserta un nuevo registro.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>Crear, modificar y quitar un desencadenador en PowerShell  
 En este ejemplo de código se muestra cómo crear e insertar un desencadenador de actualización en una tabla existente, denominada `Sales`, en la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. El desencadenador envía un mensaje de aviso cuando la tabla se actualiza o cuando se inserta un nuevo registro.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
