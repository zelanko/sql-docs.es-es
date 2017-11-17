---
title: "Crear función de AGREGADO (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad5cf36e97bf3903cc9d42ec5179de6375624f95
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una función de agregado definida por el usuario con la implementación definida en una clase de un ensamblado en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para que [!INCLUDE[ssDE](../../includes/ssde-md.md)] enlace la función de agregado con su implementación, el ensamblado de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que contiene la implementación debe cargarse primero en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una instrucción CREATE ASSEMBLY.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 Es el nombre del esquema al que pertenece la función de agregado definida por el usuario.  
  
 *aggregate_name*  
 Es el nombre de la función de agregado que desea crear.  
  
 **@***param_name*  
 Uno o más parámetros en el agregado definido por el usuario. El usuario debe proporcionar un valor del parámetro cuando se ejecute la función de agregado. Especifique un nombre de parámetro con un signo "arroba" (**@**) como primer carácter. El nombre del parámetro debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Los parámetros son locales para la función.  
  
 *system_scalar_type*  
 Es cualquiera de los tipos de datos escalares del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contienen el valor del parámetro de entrada o el valor devuelto. Todos los tipos de datos escalar se pueden utilizar como un parámetro para un agregado definido por el usuario, excepto **texto**, **ntext**, y **imagen**. Los tipos no escalares, como **cursor** y **tabla**, no se puede especificar.  
  
 *udt_schema_name*  
 Es el nombre del esquema al que pertenece el tipo definido por el usuario CLR. Si no se especifica, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] referencias *udt_type_name* en el siguiente orden:  
  
-   El espacio de nombres del tipo de SQL nativo.  
  
-   El esquema predeterminado del usuario actual en la base de datos actual.  
  
-   El esquema **dbo** de la base de datos actual.  
  
 *udt_type_name*  
 Es el nombre de un tipo definido por el usuario CLR que ya está creado en la base de datos actual. Si *udt_schema_name* no se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se supone el tipo pertenece al esquema del usuario actual.  
  
 *ASSEMBLY_NAME* [ **.** *class_name* ]  
 Especifica el ensamblado que se va a vincular con la función de agregado definida por el usuario y, opcionalmente, el nombre del esquema al que pertenece el ensamblado y el nombre de la clase del ensamblado que implementa el agregado definido por el usuario. El ensamblado debe haberse creado con antelación en la base de datos mediante una instrucción CREATE ASSEMBLY. *CLASS_NAME* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador y coincidir con el nombre de una clase que existe en el ensamblado. *CLASS_NAME* puede ser un nombre completo de espacio de nombres si el lenguaje de programación utilizado para escribir la clase utiliza espacios de nombres, como C#. Si *class_name* no se especifica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se da por supuesto es el mismo que *aggregate_name*.  
  
## <a name="remarks"></a>Comentarios  
 De manera predeterminada, la capacidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de ejecutar código CLR está desactivada. Puede crear, modificar y quitar objetos de base de datos que hagan referencia a módulos de código administrado, pero el código de estos módulos no se ejecutará en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que la [opción clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) se habilita mediante [sp_ configurar](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 La clase del ensamblado al que hace referencia en *assembly_name* y sus métodos, debe cumplir todos los requisitos para implementar una función agregada definida por el usuario en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [agregados definidos](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere premisos CREATE AGGREGATE y REFERENCES en el ensamblado que se especifica en la cláusula EXTERNAL NAME.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se da por supuesto que una aplicación de ejemplo StringUtilities.csproj está compilada. Para obtener más información, consulte [ejemplo de funciones de utilidad de cadena](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c).  
  
 En el ejemplo se crea un agregado `Concatenate`. Antes de crear el agregado, el ensamblado `StringUtilities.dll` se registra en la base de datos local.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ELIMINAR AGREGADO &#40; Transact-SQL &#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  

