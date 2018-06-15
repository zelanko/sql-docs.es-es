---
title: sp_unbindefault (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 80453657de70133f269b35387813389ecb7cff0a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262323"
---
# <a name="spunbindefault-transact-sql"></a>sp_unbindefault (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desenlaza o quita un valor predeterminado de una columna o de un tipo de datos alias en la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Le recomendamos que cree definiciones predeterminadas utilizando la palabra clave DEFAULT en la [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) instrucciones en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname=** ] **'***object_name***'**  
 Es el nombre de la tabla y columna, o el tipo de datos de alias del que se va a desenlazar el valor predeterminado. *object_name* es **nvarchar(776)**, no tiene ningún valor predeterminado. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta resolver los identificadores de dos partes en nombres de columna en primer lugar, y después en tipos de datos de alias.  
  
 Cuando se desenlaza un valor predeterminado de un tipo de datos alias, también se desenlaza cualquier columna de ese tipo de datos que tenga el mismo valor predeterminado. Las columnas de ese tipo de datos cuyos valores predeterminados estén directamente enlazados a ellas no se ven afectadas.  
  
> [!NOTE]  
>  *object_name* puede contener corchetes **[]** como caracteres de identificadores delimitados. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 [ **@futureonly=** ] **'***futureonly_flag***'**  
 Solo se usa cuando se desenlaza un valor predeterminado de un tipo de datos de alias. *futureonly_flag* es **varchar (15)**, su valor predeterminado es null. Cuando *futureonly_flag* es **futureonly**, las columnas existentes del tipo de datos no pierden el valor predeterminado especificado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Para mostrar el texto de un valor predeterminado, ejecute **sp_helptext** con el nombre del valor predeterminado como parámetro.  
  
## <a name="permissions"></a>Permissions  
 Para desenlazar un valor predeterminado de una columna de la tabla, es necesario el permiso ALTER en la tabla. Para desenlazar un valor predeterminado de un tipo de datos alias, se requiere el permiso CONTROL en el tipo o el permiso ALTER del esquema al que pertenece el tipo.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-unbinding-a-default-from-a-column"></a>A. Desenlazar un valor predeterminado de una columna  
 En el siguiente ejemplo se desenlaza el valor predeterminado de la columna `hiredate` de una tabla `employees`.  
  
```  
EXEC sp_unbindefault 'employees.hiredate';  
```  
  
### <a name="b-unbinding-a-default-from-an-alias-data-type"></a>B. Desenlazar un valor predeterminado de un tipo de datos alias  
 En el siguiente ejemplo se desenlaza el valor predeterminado del tipo de datos alias `ssn`. Desenlaza las columnas de ese tipo existentes y futuras.  
  
```  
EXEC sp_unbindefault 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. Utilizar futureonly_flag  
 En el siguiente ejemplo se desenlazan futuros usos del tipo de datos alias `ssn` sin que ello afecte a las columnas `ssn` existentes.  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. Usar identificadores delimitados  
 En el ejemplo siguiente se muestra el uso de identificadores delimitados en *object_name* parámetro.  
  
```  
CREATE TABLE [t.3] (c1 int); -- Notice the period as part of the table   
-- name.  
CREATE DEFAULT default2 AS 0;  
GO  
EXEC sp_bindefault 'default2', '[t.3].c1' ;  
-- The object contains two periods;  
-- the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
EXEC sp_unbindefault '[t.3].c1';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
