---
title: sp_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexes_TSQL
- sp_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexes
ms.assetid: 25469e72-9d95-463f-912a-193471c8f5e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b1a14d1cf8c9eac0ace93e3aac6e16219fd60eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62961917"
---
# <a name="spindexes-transact-sql"></a>sp_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información de índice para la tabla remota especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_indexes [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_db' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @table_server=] '*table_server*'  
 Es el nombre de un servidor vinculado que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el que se solicita información de tablas. *table_server* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @table_name=] '*table_name*'  
 Es el nombre de la tabla remota para la que se proporciona información de índice. *table_name* es **sysname**, su valor predeterminado es null. Si es NULL, se devuelven todas las tablas de la base de datos especificada.  
  
 [ @table_schema= ] '*table_schema*'  
 Especifica el esquema de la tabla. En el entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], corresponde al propietario de la tabla. *TABLE_SCHEMA* es **sysname**, su valor predeterminado es null.  
  
 [ @table_catalog= ] '*table_db*'  
 Es el nombre de la base de datos en el que *table_name* reside. *table_db* es **sysname**, su valor predeterminado es null. Si es NULL, *table_db* el valor predeterminado es **maestro**.  
  
 [ @index_name=] '*index_name*'  
 Es el nombre del índice para el que se solicita información. *índice* es **sysname**, su valor predeterminado es null.  
  
 [ @is_unique= ] '*is_unique*'  
 Es el tipo de índice para el que se devuelve información. *is_unique* es **bit**, su valor predeterminado es null, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|1|Devuelve información acerca de índices únicos.|  
|0|Devuelve información acerca de índices que no son únicos.|  
|NULL|Devuelve información acerca de todos los índices.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|TABLE_CAT|**sysname**|Nombre de la base de datos en que reside la tabla especificada.|  
|TABLE_SCHEM|**sysname**|Esquema de la tabla.|  
|TABLE_NAME|**sysname**|Nombre de la tabla remota.|  
|NON_UNIQUE|**smallint**|Indica si el índice es único o no:<br /><br /> 0 = Único<br /><br /> 1 = No único|  
|INDEX_QUALIFER|**sysname**|Nombre del propietario del índice. Algunos productos DBMS permiten crear índices a usuarios que no sean los propietarios de la tabla. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta columna siempre es igual a **TABLE_NAME**.|  
|INDEX_NAME|**sysname**|Nombre del índice.|  
|TYPE|**smallint**|Tipo de índice:<br /><br /> 0 = Estadísticas de una tabla<br /><br /> 1 = Clúster<br /><br /> 2 = Hash<br /><br /> 3 = Sí|  
|ORDINAL_POSITION|**int**|Posición ordinal de la columna en el índice. La primera columna del índice es 1. Esta columna siempre devuelve un valor.|  
|COLUMN_NAME|**sysname**|Es el nombre correspondiente de la columna para cada columna de TABLE_NAME devuelta.|  
|ASC_OR_DESC|**varchar**|Es el orden utilizado en la intercalación:<br /><br /> A = Ascendente<br /><br /> D = Descendente<br /><br /> NULL = No aplicable<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre devuelve A.|  
|CARDINALITY|**int**|Es el número de filas de la tabla o valores únicos del índice.|  
|PAGES|**int**|Número de páginas para el almacenamiento del índice o la tabla.|  
|FILTER_CONDITION|**nvarchar(** 4000 **)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no devuelve ningún valor.|  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve toda la información de índices de la tabla `Employees` de la base de datos `AdventureWorks2012`, que se encuentra en el servidor vinculado `Seattle1`.  
  
```  
EXEC sp_indexes @table_server = 'Seattle1',   
   @table_name = 'Employee',   
   @table_schema = 'HumanResources',  
   @table_catalog = 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vea también  
 [Distribuye los procedimientos almacenados de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
