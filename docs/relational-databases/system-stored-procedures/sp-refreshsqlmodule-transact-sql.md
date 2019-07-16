---
title: sp_refreshsqlmodule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refreshsqlmodule_TSQL
- sp_refreshsqlmodule
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- metadata [SQL Server], triggers
- metadata [SQL Server], views
- triggers [SQL Server], refreshing metadata
- views [SQL Server], refreshing metadata
- sp_refreshsqlmodule
- metadata [SQL Server], functions
- stored procedures [SQL Server], refreshing metadata
- user-defined functions [SQL Server], refreshing metadata
ms.assetid: f0022a05-50dd-4620-961d-361b1681d375
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9ed393edf79c3502bf3e054e23eb459d490ce998
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075802"
---
# <a name="sprefreshsqlmodule-transact-sql"></a>sp_refreshsqlmodule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Actualiza los metadatos para el procedimiento almacenado no enlazado a un esquema específico, función definida por el usuario, vista, desencadenador DML, desencadenador DDL de nivel de la base de datos o desencadenador DDL de nivel de servidor en la base de datos actual. Los metadatos persistentes de estos objetos, como los tipos de datos de los parámetros, pueden quedarse obsoletos debido a los cambios en sus objetos subyacentes.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_refreshsqlmodule [ @name = ] 'module_name'   
    [ , [ @namespace = ] ' <class> ' ]  
  
<class> ::=  
{  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'module\_name'` Es el nombre del procedimiento almacenado, función definida por el usuario, vista, desencadenador DML, desencadenador DDL de nivel de base de datos o desencadenador DDL de nivel de servidor. *module_name* no puede ser un common language runtime (CLR) procedimiento almacenado o una función CLR. *module_name* no puede estar enlazada a esquema. *module_name* es **nvarchar**, no tiene ningún valor predeterminado. *module_name* puede ser un identificador formado por varias partes, pero solo puede hacer referencia a objetos en la base de datos actual.  
  
`[ , @namespace = ] ' \<class> '` Es la clase del módulo especificado. Cuando *module_name* es un desencadenador DDL, \<clase > es necesario. *\<clase >* es **nvarchar**(20). Las entradas válidas son:  
  
|||  
|-|-|  
|DATABASE_DDL_TRIGGER||  
|SERVER_DDL_TRIGGER|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un número distinto de cero (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_refreshsqlmodule** se debe ejecutar cuando se realizan cambios en los objetos subyacentes del módulo que afecta a su definición. De lo contrario, el módulo podría producir resultados inesperados cuando se consulta o se invoca. Para actualizar una vista, puede usar **sp_refreshsqlmodule** o **sp_refreshview** con los mismos resultados.  
  
 **sp_refreshsqlmodule** no afecta a los permisos, las propiedades extendidas o establecer las opciones que están asociadas con el objeto.  
  
 Para actualizar un desencadenador DDL de nivel de servidor, ejecute este procedimiento almacenado desde el contexto de cualquier base de datos.  
  
> [!NOTE]  
>  Las firmas asociadas con el objeto se anulan al ejecutar **sp_refreshsqlmodule**.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER en el módulo y el permiso REFERENCES en cualquier tipo definido por el usuario CLR y las colecciones de esquemas XML a los que hace referencia el objeto. Requiere permiso ALTER ANY DATABASE DDL TRIGGER en la base de datos actual cuando el módulo especificado es un desencadenador DDL de nivel de base de datos. Requiere el permiso CONTROL SERVER cuando el módulo especificado es un desencadenador DDL de nivel de servidor.  
  
 Además, en los módulos definidos con la cláusula EXECUTE AS, es necesario el permiso IMPERSONATE en la entidad de seguridad especificada. Generalmente, al actualizar un objeto no se cambia su entidad de seguridad EXECUTE AS, a menos que el módulo se defina con EXECUTE AS USER y el nombre de usuario de la entidad de seguridad se resuelva ahora como un usuario diferente del usado en el momento en que se creó el módulo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-refreshing-a-user-defined-function"></a>A. Actualizar una función definida por el usuario  
 En el ejemplo siguiente se actualiza una función definida por el usuario. En el ejemplo se crea un tipo de datos de alias, `mytype`, y una función definida por el usuario, `to_upper`, que usa `mytype`. Entonces, el nombre de `mytype` se cambia a `myoldtype`, y se crea un nuevo `mytype` que tiene una definición diferente. La función `dbo.to_upper` se actualiza para que haga referencia a la nueva implementación de `mytype`, en lugar de a la antigua.  
  
```  
-- Create an alias type.  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT 'mytype' FROM sys.types WHERE name = 'mytype')  
DROP TYPE mytype;  
GO  
  
CREATE TYPE mytype FROM nvarchar(5);  
GO  
  
IF OBJECT_ID ('dbo.to_upper', 'FN') IS NOT NULL  
DROP FUNCTION dbo.to_upper;  
GO  
  
CREATE FUNCTION dbo.to_upper (@a mytype)  
RETURNS mytype  
WITH ENCRYPTION  
AS  
BEGIN  
RETURN upper(@a)  
END;  
GO  
  
SELECT dbo.to_upper('abcde');  
GO  
  
-- Increase the length of the alias type.  
sp_rename 'mytype', 'myoldtype', 'userdatatype';  
GO  
  
CREATE TYPE mytype FROM nvarchar(10);  
GO  
  
-- The function parameter still uses the old type.  
SELECT name, type_name(user_type_id)   
FROM sys.parameters   
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh'); -- Fails because of truncation  
GO  
  
-- Refresh the function to bind to the renamed type.  
EXEC sys.sp_refreshsqlmodule 'dbo.to_upper';  
  
-- The function parameters are now bound to the correct type and the statement works correctly.  
SELECT name, type_name(user_type_id) FROM sys.parameters  
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh');  
GO  
```  
  
### <a name="b-refreshing-a-database-level-ddl-trigger"></a>b. Actualizar un desencadenador DDL de nivel de la base de datos  
 El ejemplo siguiente actualiza un desencadenador DDL de nivel de la base de datos.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddlDatabaseTriggerLog' , @namespace = 'DATABASE_DDL_TRIGGER';  
GO  
```  
  
### <a name="c-refreshing-a-server-level-ddl-trigger"></a>C. Actualizar un desencadenador DDL de nivel de servidor  
 El ejemplo siguiente actualiza un desencadenador DDL de nivel de servidor.  
  
||  
|-|  
|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
```  
USE master;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddl_trig_database' , @namespace = 'SERVER_DDL_TRIGGER';  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_refreshview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
