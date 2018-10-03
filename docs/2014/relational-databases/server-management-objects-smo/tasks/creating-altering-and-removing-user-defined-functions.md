---
title: Crear, modificar y quitar funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ced5a796739ea508440fea9ddbb645443fdda786
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054505"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>Crear, modificar y eliminar las funciones definidas por el usuario
  El <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto proporciona la funcionalidad que permite a los usuarios administrar mediante programación las funciones definidas por el usuario en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las funciones definidas por el usuario admiten los parámetros de entrada y salida y también admiten las referencias directas a las columnas de la tabla.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requiere registrar dentro de una base de datos antes de que se los ensamblados se pueden usar los procedimientos almacenados, tipos de datos definidos por el usuario, desencadenadores y funciones definidas por el usuario. SMO admite esta característica con el objeto <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly>.  
  
 El <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto hace referencia al ensamblado de .NET con el <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A>, y <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A> propiedades.  
  
 Cuando el <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> objeto hace referencia a un ensamblado. NET, debe registrar el ensamblado mediante la creación de un <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> objeto y agregarla a la <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> objeto, que pertenece a la <xref:Microsoft.SqlServer.Management.Smo.Database> objeto.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) o [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Crear una función escalar definida por el usuario en Visual Basic  
 Este ejemplo de código muestra cómo crear y quitar una función escalar definida por el usuario que tiene una entrada <xref:System.DateTime> parámetro de objeto y un entero de devuelven el tipo en [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. La función definida por el usuario se crea en el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos. En el ejemplo se crea una función definida por el usuario, ISOweek, que toma un argumento de fecha y calcula el número de semana ISO. Para que esta función realice los cálculos correctamente, la opción DATEFIRST de base de datos debe establecerse en 1 antes de que se llame a la función.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Crear una función escalar definida por el usuario en Visual C#  
 Este ejemplo de código muestra cómo crear y quitar una función escalar definida por el usuario que tiene una entrada <xref:System.DateTime> parámetro de objeto y un entero de devuelven el tipo en [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. La función definida por el usuario se crea en el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos. En el ejemplo se crea la función definida por el usuario. `ISOweek`  Esta función toma un argumento de fecha para calcular el número de semana ISO. Para que esta función realice los cálculos correctamente, la opción `DATEFIRST` de base de datos debe establecerse en `1` antes de que se llame a la función.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>Crear una función escalar definida por el usuario en PowerShell  
 Este ejemplo de código muestra cómo crear y quitar una función escalar definida por el usuario que tiene una entrada <xref:System.DateTime> parámetro de objeto y un entero de devuelven el tipo en [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]. La función definida por el usuario se crea en el [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] base de datos. En el ejemplo se crea la función definida por el usuario. `ISOweek`  Esta función toma un argumento de fecha para calcular el número de semana ISO. Para que esta función realice los cálculos correctamente, la opción `DATEFIRST` de base de datos debe establecerse en `1` antes de que se llame a la función.  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.   
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.   
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int   
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.   
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.   
$udf.Create()  
  
# Remove the user-defined function.   
$udf.Drop()  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
  
  
