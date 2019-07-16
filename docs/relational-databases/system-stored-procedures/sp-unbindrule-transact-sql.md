---
title: sp_unbindrule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
author: stevestein
ms.author: sstein
ms.openlocfilehash: b409b76d3a7c07ac03173346059f38ac616f5a87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095860"
---
# <a name="spunbindrule-transact-sql"></a>sp_unbindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deshace el enlace de una regla de una columna o de un tipo de datos del alias en la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Se recomienda crear definiciones predeterminadas utilizando la palabra clave DEFAULT en la [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) instrucciones en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @objname = ] 'object_name'` Es el nombre de la tabla y columna o el tipo de datos de alias desde el que la regla está desenlazada. *object_name* es **nvarchar(776)** , no tiene ningún valor predeterminado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta resolver los identificadores de dos partes en nombres de columna en primer lugar, y después en tipos de datos de alias. Cuando se deshace el enlace de una regla de un tipo de datos de alias, también se deshace el enlace de las columnas de ese tipo de datos que tengan la misma regla. Las columnas de ese tipo de datos con reglas directamente enlazadas a ellas no se ven afectadas.  
  
> [!NOTE]  
>  *object_name* puede contener corchetes **[]** como caracteres de identificadores delimitados. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
`[ @futureonly = ] 'futureonly_flag'` Se usa solo cuando se desenlaza una regla de un tipo de datos de alias. *futureonly_flag* es **varchar (15)** , su valor predeterminado es null. Cuando *futureonly_flag* es **futureonly**, las columnas existentes de ese tipo de datos no pierden la regla especificada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Para que se muestre el texto de una regla, ejecute **sp_helptext** con el nombre de la regla como parámetro.  
  
 Cuando una regla está enlazada, se quita la información sobre el enlace de la **sys.columns** tabla si la regla estaba enlazada a una columna y desde el **sys.types** si la regla estaba enlazada a un tipo de datos de alias de tabla.  
  
 Cuando se deshace el enlace de una regla de un tipo de datos de alias, también se deshace el enlace de las columnas que tengan ese tipo de datos de alias. La regla también todavía puede estar enlazada a columnas cuyos tipos de datos se han cambiado posteriormente mediante la cláusula ALTER COLUMN de una instrucción ALTER TABLE, específicamente debe desenlazar la regla de estas columnas mediante **sp_unbindrule** y especificando el nombre de columna.  
  
## <a name="permissions"></a>Permisos  
 Para deshacer el enlace de una regla de una columna de tabla es necesario el permiso ALTER para la tabla. Para deshacer el enlace de una regla de un tipo de datos de alias es necesario el permiso CONTROL para el tipo o el permiso ALTER para el esquema al que pertenece el tipo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>A. Desenlazar una regla de una columna  
 En el siguiente ejemplo se deshace el enlace de la columna `startdate` de una tabla `employees`.  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>b. Desenlazar una regla de un tipo de datos de alias  
 En el siguiente ejemplo se deshace el enlace de la regla del tipo de datos de alias `ssn`. Deshace el enlace de la regla de las columnas de ese tipo existentes y futuras.  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonlyflag"></a>C. Utilizar futureonly_flag  
 En el siguiente ejemplo se deshace el enlace de la regla del tipo de datos de alias `ssn` sin afectar a las columnas `ssn` existentes.  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Uso de identificadores delimitados  
 El ejemplo siguiente muestra el uso de identificadores delimitados en los *object_name* parámetro.  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
