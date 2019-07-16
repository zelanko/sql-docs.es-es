---
title: sp_bindrule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76d1572e1f99162c8daebeafadb0c8d75a53a4d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046028"
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Enlaza una regla a una columna o a un tipo de datos de alias.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use[restricciones Unique y restricciones Check](../../relational-databases/tables/unique-constraints-and-check-constraints.md) en su lugar. Las restricciones CHECK se crean mediante el uso de la palabra clave CHECK de la [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) o [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) instrucciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rulename = ] 'rule'` Es el nombre de una regla creada con la instrucción CREATE RULE. *regla* es **nvarchar(776)** , no tiene ningún valor predeterminado.  
  
`[ @objname = ] 'object_name'` Es la tabla y columna o a la que la regla es enlazar el tipo de datos de alias. Una regla no se puede enlazar a una columna **text**, **ntext**, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **xml**, de tipo definido por el usuario CLR o **timestamp**. Una regla no se puede enlazar a una columna calculada.  
  
 *object_name* es **nvarchar(776)** no tiene ningún valor predeterminado. Si *object_name* es un nombre de una parte, se resuelve como un tipo de datos de alias. Si es un nombre de dos o tres partes, se resuelve primero como una tabla y una columna, y si esta resolución genera un error, se resuelve como un tipo de datos de alias. De forma predeterminada, las columnas existentes del tipo de datos de alias heredan *regla* a menos que se ha enlazado una regla directamente a la columna.  
  
> [!NOTE]  
>  *object_name* puede contener corchetes **[** y **]** caracteres como caracteres de identificador delimitado. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Las reglas creadas a partir de expresiones que utilizan tipos de datos de alias pueden enlazarse a columnas o tipos de datos de alias, pero no se compilan cuando se hace referencia a ellos. Evite el uso de reglas creadas a partir de tipos de datos de alias.  
  
`[ @futureonly = ] 'futureonly_flag'` Se usa sólo cuando se enlaza una regla a un tipo de datos de alias. *future_only_flag* es **varchar (15)** con el valor predeterminado es NULL. Este parámetro cuando se establece en **futureonly** impide que las columnas existentes de un tipo de datos de alias hereden la nueva regla. Si *futureonly_flag* es NULL, la nueva regla se enlaza con las columnas del tipo de datos de alias que actualmente no tengan regla o utilicen la regla existente del tipo de datos de alias.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Puede enlazar una regla nueva a una columna (aunque es preferible usar una restricción CHECK) o a un tipo de datos de alias con **sp_bindrule** sin desenlazar una regla existente. Se reemplaza la regla anterior. Si se enlaza una regla a una columna con una restricción CHECK existente, se evalúan todas las restricciones. No se puede enlazar una regla a un tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La regla se aplica cuando se intenta ejecutar una instrucción INSERT, no en la operación de enlace. Puede enlazar una regla de caracteres a una columna de **numérico** tipo de datos, aunque este tipo de operación de INSERCIÓN no es válido.  
  
 Las columnas existentes del tipo de datos de alias heredan la nueva regla a menos que *futureonly_flag* se especifica como **futureonly**. Las nuevas columnas definidas con el tipo de datos de alias siempre heredan la regla. Sin embargo, si la cláusula ALTER COLUMN de una instrucción ALTER TABLE cambia el tipo de datos de una columna a un tipo de datos de alias enlazado a una regla, la columna no hereda la regla enlazada al tipo de datos. La regla se debe enlazar específicamente a la columna mediante el uso de **sp_bindrule**.  
  
 Al enlazar una regla a una columna, la información relacionada se agrega a la **sys.columns** tabla. Al enlazar una regla a un tipo de datos de alias, la información relacionada se agrega a la **sys.types** tabla.  
  
## <a name="permissions"></a>Permisos  
 Para enlazar una regla a una columna de una tabla, se debe tener el permiso ALTER en la tabla. Se requiere el permiso CONTROL en el tipo de datos de alias, o el permiso ALTER en el esquema al que pertenece el tipo, para enlazar una regla a un tipo de datos de alias.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. Enlazar una regla a una columna  
 Partiendo de la base de que se ha creado una regla denominada `today` en la base de datos actual mediante la instrucción CREATE RULE, este ejemplo enlaza la regla a la columna `HireDate` de la tabla `Employee`. Cuando se agrega una fila a `Employee`, los datos de la columna `HireDate` se comprueban con la regla `today`.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>b. Enlazar una regla a un tipo de datos de alias  
 Suponiendo que existe una regla denominada `rule_ssn` y un tipo de datos de alias denominado `ssn`, este ejemplo enlaza `rule_ssn` a `ssn`. En una instrucción CREATE TABLE, las columnas del tipo `ssn` heredan la regla `rule_ssn`. Las columnas existentes del tipo `ssn` también heredan la `rule_ssn` de regla, a menos que **futureonly** se especifica para *futureonly_flag*, o `ssn` tenga una regla enlazada directamente a él. Las reglas enlazadas a columnas siempre tienen prioridad sobre las enlazadas a tipos de datos.  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Utilizar futureonly_flag  
 En el ejemplo siguiente se enlaza la regla `rule_ssn` al tipo de datos de alias `ssn`. Como se especifica `futureonly`, esto no afecta a ninguna de las columnas existentes de tipo `ssn`.  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Uso de identificadores delimitados  
 El ejemplo siguiente muestra el uso de identificadores delimitados en *object_name* parámetro.  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
