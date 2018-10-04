---
title: Trabajar con tipos de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a649e00e5b77a7b3276e82e34c04657cd8307284
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121585"
---
# <a name="working-with-data-types"></a>Trabajar con tipos de datos
  Los datos se presentan en diversos tipos y tamaños como, por ejemplo, una cadena con una longitud definida, un número con una precisión específica o un tipo de datos definido por el usuario que es otro objeto que tiene su propio conjunto de reglas. El <xref:Microsoft.SqlServer.Management.Smo.DataType> objeto clasifica el tipo de datos para que se pueda administrar correctamente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> está asociada a objetos que aceptan datos. La siguiente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) aceptan datos que deben estar definidos por un <xref:Microsoft.SqlServer.Management.Smo.DataType> propiedad de objeto:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 La propiedad `DataType` de los objetos que aceptan los datos puede establecerse de varias formas.  
  
-   Utilice el constructor predeterminado y especifique <xref:Microsoft.SqlServer.Management.Smo.DataType> explícitamente propiedades del objeto  
  
-   Use un constructor sobrecargado y especifique el <xref:Microsoft.SqlServer.Management.Smo.DataType> propiedades como parámetros.  
  
-   Especifique el <xref:Microsoft.SqlServer.Management.Smo.DataType> insertado en el constructor del objeto.  
  
-   Use uno de los miembros estáticos de la clase <xref:Microsoft.SqlServer.Management.Smo.DataType> como, por ejemplo, `Int`. De esta forma, se devolverá una instancia de un objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>.  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> tiene varias propiedades que definen el tipo de datos. Por ejemplo, la propiedad <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> especifica el tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los valores constantes que representan [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se enumeran los tipos de datos en el <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> enumeración. Se trata de tipos de datos como `varchar`, `nchar`, `currency`, `integer`, `float` y `datetime`.  
  
 Al establecer el tipo de datos, deben establecerse propiedades concretas para los datos. Por ejemplo, si es un tipo `nchar`, la longitud de los datos de cadena debe establecerse en la propiedad `Length`. Esto mismo se aplica a los valores numéricos, en los que debe especificarse una precisión y una escala.  
  
 Los tipos de datos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> y <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> hacen referencia a objetos que contienen la definición del tipo de datos definido por el usuario. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> se basa en los tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de la enumeración <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>. El <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> se basa en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipos de datos. NET. Normalmente, representarían datos de un tipo específico que la base de datos reutiliza con frecuencia debido a las reglas de negocios definidas por la organización. Por ejemplo, un tipo de datos que almacena una cantidad de dinero y un denominador de divisa resultarían de gran utilidad en una compañía que trabaje con distintas divisas.  
  
 El <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> enumeración contiene una lista de todos los [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-tipos de datos admitidos.  
  
## <a name="examples"></a>Ejemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Construir un objeto DataType con la especificación del constructor de Visual Basic  
 Este ejemplo de código muestra cómo utilizar el constructor para crear instancias de tipos de datos que se basan en diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.  
  
> [!NOTE]  
>  Los tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> y XML exigen, todos ellos, un valor de nombre que identifique el objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Construir un objeto DataType con la especificación del constructor de Visual Basic C#  
 Este ejemplo de código muestra cómo utilizar el constructor para crear instancias de tipos de datos que se basan en diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.  
  
> [!NOTE]  
>  Los tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> y XML exigen, todos ellos, un valor de nombre que identifique el objeto.  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguements specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Construir un objeto DataType utilizando el constructor predeterminado de Visual Basic  
 Este ejemplo de código muestra cómo usar el constructor predeterminado para crear instancias de tipos de datos que se basan en diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos. Después, las propiedades se utilizan para especificar el tipo de datos.  
  
 **Tenga en cuenta** el <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, y todos los tipos XML requieren un valor de nombre para identificar el objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Construir un objeto DataType utilizando el constructor predeterminado de Visual C#  
 Este ejemplo de código muestra cómo usar el constructor predeterminado para crear instancias de tipos de datos que se basan en diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos. Después, las propiedades se utilizan para especificar el tipo de datos.  
  
 **Tenga en cuenta** el <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, y todos los tipos XML requieren un valor de nombre para identificar el objeto.  
  
```  
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
  
  
