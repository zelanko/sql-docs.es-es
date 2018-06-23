---
title: Crear, modificar y eliminar los procedimientos almacenados | Documentos de Microsoft
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
- stored procedures [SMO]
ms.assetid: 2a072f9c-8f11-4364-ab71-3990735a8d66
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 18ab85b6ea304660e412e0e0156fcc1cc9491fc3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104206"
---
# <a name="creating-altering-and-removing-stored-procedures"></a>Crear, modificar y eliminar los procedimientos almacenados
  En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), los procedimientos almacenados se representan mediante la <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> objeto.  
  
 Crear un <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> objeto SMO requiere la configuración del <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.TextBody%2A> propiedad a la [!INCLUDE[tsql](../../../includes/tsql-md.md)] script que define el procedimiento almacenado. Los parámetros requieren el prefijo @ y se deben crear individualmente utilizando los objetos <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> y agregando a la colección <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> del objeto <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear a Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-basic"></a>Crear, modificar y eliminar un procedimiento almacenado en Visual Basic  
 Este ejemplo de código muestra cómo crear un procedimiento almacenado para el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos. El ejemplo devuelve el apellido de un empleado cuando se proporciona el número de identificador del empleado. El procedimiento almacenado requiere un parámetro de entrada que especifique el número de identificador del empleado y un parámetro de salida para devolver el apellido del empleado.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStoredProcs1](SMO How to#SMO_VBStoredProcs1)]  -->  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-c"></a>Crear, modificar y eliminar un procedimiento almacenado en Visual C#  
 Este ejemplo de código muestra cómo crear un procedimiento almacenado para el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos. El ejemplo devuelve el apellido de un empleado cuando se proporciona el número de identificador del empleado (`BusinessEntityID`). El procedimiento almacenado requiere un parámetro de entrada que especifique el número de identificador del empleado y un parámetro de salida para devolver el apellido del empleado.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
            StoredProcedure sp;  
            sp = new StoredProcedure(db, "GetLastNameByBusinessEntityID");  
            //Set the TextMode property to false and then set the other object properties.   
            sp.TextMode = false;  
            sp.AnsiNullsStatus = false;  
            sp.QuotedIdentifierStatus = false;  
            //Add two parameters.   
            StoredProcedureParameter param;  
            param = new StoredProcedureParameter(sp, "@empval", DataType.Int);  
            sp.Parameters.Add(param);  
            StoredProcedureParameter param2;  
            param2 = new StoredProcedureParameter(sp, "@retval", DataType.NVarChar(50));  
            param2.IsOutputParameter = true;  
            sp.Parameters.Add(param2);  
            //Set the TextBody property to define the stored procedure.   
            string stmt;  
            stmt = " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )";  
            sp.TextBody = stmt;  
            //Create the stored procedure on the instance of SQL Server.   
            sp.Create();  
            //Modify a property and run the Alter method to make the change on the instance of SQL Server.   
            sp.QuotedIdentifierStatus = true;  
            sp.Alter();  
            //Remove the stored procedure.   
            sp.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-powershell"></a>Crear, modificar y eliminar un procedimiento almacenado en PowerShell  
 Este ejemplo de código muestra cómo crear un procedimiento almacenado para el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos. El ejemplo devuelve el apellido de un empleado cuando se proporciona el número de identificador del empleado (`BusinessEntityID`). El procedimiento almacenado requiere un parámetro de entrada que especifique el número de identificador del empleado y un parámetro de salida para devolver el apellido del empleado.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
$sp  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedure `  
-argumentlist $db, "GetLastNameByBusinessEntityID"  
  
#Set the TextMode property to false and then set the other object properties.   
$sp.TextMode = $false  
$sp.AnsiNullsStatus = $false  
$sp.QuotedIdentifierStatus = $false  
  
# Add two parameters  
$type = [Microsoft.SqlServer.Management.SMO.Datatype]::Int  
$param  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@empval",$type  
$sp.Parameters.Add($param)  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::NVarChar(50)  
$param2  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@retval",$type  
$param2.IsOutputParameter = $true  
$sp.Parameters.Add($param2)  
  
#Set the TextBody property to define the stored procedure.   
$sp.TextBody =  " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )"  
  
# Create the stored procedure on the instance of SQL Server.   
$sp.Create()  
  
# Modify a property and run the Alter method to make the change on the instance of SQL Server.   
$sp.QuotedIdentifierStatus = $true  
$sp.Alter()  
  
#Remove the stored procedure.   
$sp.Drop()  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>  
  
  