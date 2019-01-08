---
title: Crear, modificar y quitar procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [SMO]
ms.assetid: 2a072f9c-8f11-4364-ab71-3990735a8d66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc38e4f11b32c368626b0f84a352d3f9c00fa0f7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805417"
---
# <a name="creating-altering-and-removing-stored-procedures"></a>Crear, modificar y eliminar los procedimientos almacenados
  En los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO), el objeto <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> representa los procedimientos almacenados.  
  
 Para crear un objeto <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> en SMO, se requiere establecer la propiedad <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.TextBody%2A> en el script [!INCLUDE[tsql](../../../includes/tsql-md.md)] que define el procedimiento almacenado. Los parámetros requieren el \@ prefijo y se deben crear individualmente utilizando <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> objetos y agregar a la <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> colección de la <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> objeto.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-basic"></a>Crear, modificar y eliminar un procedimiento almacenado en Visual Basic  
 En este ejemplo de código se muestra cómo crear un procedimiento almacenado para la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . El ejemplo devuelve el apellido de un empleado cuando se proporciona el número de identificador del empleado. El procedimiento almacenado requiere un parámetro de entrada que especifique el número de identificador del empleado y un parámetro de salida para devolver el apellido del empleado.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStoredProcs1](SMO How to#SMO_VBStoredProcs1)]  -->  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-c"></a>Crear, modificar y eliminar un procedimiento almacenado en Visual C#  
 En este ejemplo de código se muestra cómo crear un procedimiento almacenado para la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . El ejemplo devuelve el apellido de un empleado cuando se proporciona el número de identificador del empleado (`BusinessEntityID`). El procedimiento almacenado requiere un parámetro de entrada que especifique el número de identificador del empleado y un parámetro de salida para devolver el apellido del empleado.  
  
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
 En este ejemplo de código se muestra cómo crear un procedimiento almacenado para la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . El ejemplo devuelve el apellido de un empleado cuando se proporciona el número de identificador del empleado (`BusinessEntityID`). El procedimiento almacenado requiere un parámetro de entrada que especifique el número de identificador del empleado y un parámetro de salida para devolver el apellido del empleado.  
  
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
  
  
