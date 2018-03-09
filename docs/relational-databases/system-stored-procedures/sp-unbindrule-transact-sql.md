---
title: sp_unbindrule (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 587578e7b9133b5323557b6cd1b5246a148bcb6e
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spunbindrule-transact-sql"></a>sp_unbindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deshace el enlace de una regla de una columna o de un tipo de datos del alias en la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]Le recomendamos que cree definiciones predeterminadas utilizando la palabra clave DEFAULT en la [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) instrucciones en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=** ] **'***object_name***'**  
 Es el nombre de la tabla y de la columna o el tipo de datos del alias del que se tiene que desenlazar la regla. *object_name* es **nvarchar(776)**, no tiene ningún valor predeterminado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta resolver los identificadores de dos partes en nombres de columna en primer lugar, y después en tipos de datos de alias. Cuando se deshace el enlace de una regla de un tipo de datos de alias, también se deshace el enlace de las columnas de ese tipo de datos que tengan la misma regla. Las columnas de ese tipo de datos con reglas directamente enlazadas a ellas no se ven afectadas.  
  
> [!NOTE]  
>  *object_name* puede contener corchetes **[]** como caracteres de identificadores delimitados. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 [  **@futureonly=** ] **'***futureonly_flag***'**  
 Solo se usa cuando se desenlaza una regla de un tipo de datos de alias. *futureonly_flag* es **varchar (15)**, su valor predeterminado es null. Cuando *futureonly_flag* es **futureonly**, las columnas existentes de ese tipo de datos no pierden la regla especificada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Para mostrar el texto de una regla, ejecute **sp_helptext** con el nombre de la regla como parámetro.  
  
 Cuando tiene que desenlazar una regla, se quita la información sobre el enlace de la **sys.columns** tabla si la regla estaba enlazada a una columna y de la **sys.types** si la regla estaba enlazada a un tipo de datos de alias de tabla.  
  
 Cuando se deshace el enlace de una regla de un tipo de datos de alias, también se deshace el enlace de las columnas que tengan ese tipo de datos de alias. La regla también todavía puede estar enlazada a columnas cuyos tipos de datos se han cambiado posteriormente mediante la cláusula ALTER COLUMN de una instrucción ALTER TABLE, específicamente debe desenlazar la regla de estas columnas mediante **sp_unbindrule** y especificando el nombre de columna.  
  
## <a name="permissions"></a>Permissions  
 Para deshacer el enlace de una regla de una columna de tabla es necesario el permiso ALTER para la tabla. Para deshacer el enlace de una regla de un tipo de datos de alias es necesario el permiso CONTROL para el tipo o el permiso ALTER para el esquema al que pertenece el tipo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>A. Desenlazar una regla de una columna  
 En el siguiente ejemplo se deshace el enlace de la columna `startdate` de una tabla `employees`.  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>B. Desenlazar una regla de un tipo de datos de alias  
 En el siguiente ejemplo se deshace el enlace de la regla del tipo de datos de alias `ssn`. Deshace el enlace de la regla de las columnas de ese tipo existentes y futuras.  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonlyflag"></a>C. Utilizar futureonly_flag  
 En el siguiente ejemplo se deshace el enlace de la regla del tipo de datos de alias `ssn` sin afectar a las columnas `ssn` existentes.  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usar identificadores delimitados  
 En el ejemplo siguiente se muestra el uso de identificadores delimitados en el *object_name* parámetro.  
  
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
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [Eliminar regla &#40; Transact-SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
