---
description: Trabajar con tipos de datos
title: Trabajar con tipos de datos | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 99ac0e206244404d1f4155acdd10c0a35df6e719
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420309"
---
# <a name="working-with-data-types"></a>Trabajar con tipos de datos
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Los datos se presentan en diversos tipos y tamaños como, por ejemplo, una cadena con una longitud definida, un número con una precisión específica o un tipo de datos definido por el usuario que es otro objeto que tiene su propio conjunto de reglas. El <xref:Microsoft.SqlServer.Management.Smo.DataType> objeto clasifica el tipo de datos para que pueda controlarse correctamente mediante [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> está asociada a objetos que aceptan datos. Los siguientes objetos SMO (objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) aceptan datos que deben definirse mediante una propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 La propiedad **DataType** de los objetos que aceptan los datos puede establecerse de varias formas.  
  
-   Use el constructor predeterminado y especifique las propiedades de objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> de forma explícita.  
  
-   Use un constructor sobrecargado y especifique las propiedades <xref:Microsoft.SqlServer.Management.Smo.DataType> como parámetros.  
  
-   Especifique el objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> insertado en el constructor de objeto.  
  
-   Use uno de los miembros estáticos de la <xref:Microsoft.SqlServer.Management.Smo.DataType> clase, por ejemplo **int**. De hecho, Esto devolverá una instancia de un <xref:Microsoft.SqlServer.Management.Smo.DataType> objeto.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> tiene varias propiedades que definen el tipo de datos. Por ejemplo, la propiedad <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> especifica el tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los valores constantes que representan los tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se relacionan en la enumeración <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>. Se trata de tipos de datos como **varchar**, **nchar**, **currency**, **integer**, **float**y **datetime**.  
  
 Al establecer el tipo de datos, deben establecerse propiedades concretas para los datos. Por ejemplo, si es un tipo **nchar** , la longitud de los datos de cadena debe establecerse en la propiedad **Length** . Esto mismo se aplica a los valores numéricos, en los que debe especificarse una precisión y una escala.  
  
 Los tipos de datos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> y <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> hacen referencia a objetos que contienen la definición del tipo de datos definido por el usuario. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> se basa en los tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de la enumeración <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>Se basa en los [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipos de datos de .net. Normalmente, representarían datos de un tipo específico que la base de datos reutiliza con frecuencia debido a las reglas de negocios definidas por la organización. Por ejemplo, un tipo de datos que almacena una cantidad de dinero y un denominador de divisa resultarían de gran utilidad en una compañía que trabaje con distintas divisas.  
  
 La enumeración <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> contiene una lista de todos los tipos de datos compatibles con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Construir un objeto DataType con la especificación del constructor de Visual Basic  
 En este ejemplo de código se muestra cómo utilizar el constructor para crear instancias de tipos de datos basadas en tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferentes.  
  
> [!NOTE]  
>  Los tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> y XML exigen, todos ellos, un valor de nombre que identifique el objeto.  
  
```VBNET
'Declare a DataType object variable and define the data type in the constructor.
Dim dt As DataType
'For the decimal data type the following two arguments specify precision, and scale.
dt = New DataType(SqlDataType.Decimal, 10, 2)
``` 
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Construir un objeto DataType con la especificación del constructor de Visual Basic C#  
 En este ejemplo de código se muestra cómo utilizar el constructor para crear instancias de tipos de datos basadas en tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferentes.  
  
> [!NOTE]  
>  Los tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> y XML exigen, todos ellos, un valor de nombre que identifique el objeto.  
  
```csharp  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguments specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Construir un objeto DataType utilizando el constructor predeterminado de Visual Basic  
 En este ejemplo de código se muestra cómo utilizar el constructor predeterminado para crear instancias de tipos de datos basadas en tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferentes. Después, las propiedades se utilizan para especificar el tipo de datos.  
  
 **Nota:** Los <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> tipos de XML, y requieren un valor de nombre para identificar el objeto.  
  
```VBNET
'Declare and create a DataType object variable.
Dim dt As DataType
dt = New DataType
'Define the data type by setting the SqlDataType property.
dt.SqlDataType = SqlDataType.VarChar
'The VarChar data type requires a value for the MaximumLength property.
dt.MaximumLength = 100
```
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Construir un objeto DataType utilizando el constructor predeterminado de Visual C#  
 En este ejemplo de código se muestra cómo utilizar el constructor predeterminado para crear instancias de tipos de datos basadas en tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferentes. Después, las propiedades se utilizan para especificar el tipo de datos.  
  
 **Nota:** Los <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> tipos de XML, y requieren un valor de nombre para identificar el objeto.  
  
```csharp  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
