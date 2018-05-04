---
title: sp_bindefault (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 67d46825f0da450707710c600cacb549d370082c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spbindefault-transact-sql"></a>sp_bindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enlaza un valor predeterminado con una columna o un tipo de datos de alias.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Le recomendamos que cree definiciones predeterminadas utilizando la palabra clave DEFAULT de la [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) instrucciones en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@defname=** ] **'***predeterminado***'**  
 Es el nombre del valor predeterminado creado por CREATE DEFAULT. *valor predeterminado* es **nvarchar(776)**, no tiene ningún valor predeterminado.  
  
 [  **@objname=** ] **'***object_name***'**  
 Es el nombre de la tabla y columna, o el tipo de datos de alias al que se va a enlazar el valor predeterminado. *object_name* es **nvarchar(776)** no tiene ningún valor predeterminado. *object_name* no se pueden definir con la **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, o CLR tipos definidos por el usuario.  
  
 Si *object_name* es un nombre de una parte, se resuelve como un tipo de datos de alias. Si es un nombre de dos o tres partes, se resuelve primero como una tabla y columna; y si se produce un error en esta solución, se resuelve como un tipo de datos de alias. De forma predeterminada, las columnas existentes del tipo de datos de alias heredan *predeterminado*, a menos que el valor predeterminado se ha enlazado directamente a la columna. No se puede enlazar un valor predeterminado para un **texto**, **ntext**, **imagen**, **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **marca de tiempo**, o CLR columna de tipo definido por el usuario, una columna con la propiedad IDENTITY, una columna calculada o una columna que ya tiene una restricción DEFAULT.  
  
> [!NOTE]  
>  *object_name* puede contener corchetes **[]** como identificadores delimitados. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 [ **@futureonly=** ] **'***futureonly_flag***'**  
 Solo se usa cuando se enlaza un valor predeterminado a un tipo de datos de alias. *futureonly_flag* es **varchar (15)** con un valor predeterminado es NULL. Cuando este parámetro se establece en **futureonly**, las columnas existentes de ese tipo de datos no pueden heredar el nuevo valor predeterminado. Este parámetro nunca se utiliza al enlazar un valor predeterminado con una columna. Si *futureonly_flag* es NULL, el nuevo valor predeterminado se enlaza con las columnas del tipo de datos de alias que actualmente no tiene ningún valor predeterminado o que utilizan el valor predeterminado existente del tipo de datos del alias.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Puede usar **sp_bindefault** para enlazar un nuevo valor predeterminado a una columna, aunque es preferible el uso de la restricción predeterminada, o a un tipo de datos de alias sin desenlazar un valor predeterminado existente. El valor predeterminado anterior se reemplaza. No puede enlazar un valor predeterminado con un tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un tipo definido por el usuario CLR. Si el valor predeterminado no es compatible con la columna con la que se debe enlazar, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] devuelve un mensaje de error cuando intenta insertar el valor predeterminado y no cuando lo enlaza.  
  
 Las columnas existentes del tipo de datos de alias heredan el nuevo valor predeterminado, a menos que tengan un valor predeterminado se enlaza directamente con ellos o *futureonly_flag* se especifica como **futureonly**. Las nuevas columnas del tipo de datos de alias siempre heredan el valor predeterminado.  
  
 Al enlazar un valor predeterminado a una columna, la información relacionada se agrega a la **sys.columns** vista de catálogo. Al enlazar un valor predeterminado a un tipo de datos de alias, la información relacionada se agrega a la **sys.types** vista de catálogo.  
  
## <a name="permissions"></a>Permissions  
 Usuario debe poseer la tabla o ser un miembro de la **sysadmin** fija de servidor sysadmin o el **db_owner** y **db_ddladmin** funciones fijas de base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-binding-a-default-to-a-column"></a>A. Enlazar un valor predeterminado con una columna  
 Se ha definido un valor predeterminado denominado `today` en la base de datos actual mediante CREATE DEFAULT y en el siguiente ejemplo se enlaza el valor predeterminado con la columna `HireDate` de la tabla `Employee`. Cuando se agregue una fila a la tabla `Employee` y no se proporcionen datos para la columna `HireDate`, dicha columna obtiene el valor predeterminado `today`.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. Enlazar un valor predeterminado con un tipo de datos de alias  
 El valor predeterminado denominado `def_ssn` y el tipo de datos de alias denominado `ssn` ya existen. En el siguiente ejemplo se enlaza el valor predeterminado `def_ssn` con `ssn`. Al crear una tabla, el valor predeterminado es heredado por todas las columnas a las que se asigna el tipo de datos de alias `ssn`. Las columnas existentes de tipo **ssn** también heredan el valor predeterminado **def_ssn**, a menos que **futureonly** especificado para *futureonly_flag* valor, o bien, a menos que la columna tiene un valor predeterminado enlazado directamente a él. Los valores predeterminados enlazados con columnas siempre tienen preferencia sobre los enlazados con tipos de datos.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Utilizar futureonly_flag  
 En el siguiente ejemplo se enlaza el valor predeterminado `def_ssn` con el tipo de datos de alias `ssn`. Dado que **futureonly** se especifica, no las columnas existentes del tipo `ssn` se ven afectados.  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usar identificadores delimitados  
 En el ejemplo siguiente se muestra el uso de identificadores delimitados, `[t.1]`, en *object_name*.  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
