---
title: DB_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs:
- TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b445816ec9d088138d17c103f39f1471ce16c57c
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786816"
---
# <a name="dbid-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve el número de identificación de base de datos de una base de datos especificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
'*database_name*'  
El nombre de la base de datos cuyo número de identificación de base de datos devolverá `DB_ID`. Si la llamada a `DB_ID` omite *database_name*, `DB_ID` devuelve el identificador de la base de datos actual.
  
## <a name="return-types"></a>Tipos de valores devueltos
**int**

## <a name="remarks"></a>Notas
`DB_ID` solo se puede usar para devolver el identificador de la base de datos actual de Azure SQL Database. Se devuelve NULL si el nombre de la base de datos que especificó es distinto de la base de datos actual.
  
## <a name="permissions"></a>Permisos  
Si el autor de la llamada de `DB_ID` no posee una base de datos **master** o distinta de **tempdb** determinada, como mínimo se requieren los permisos `ALTER ANY DATABASE` o `VIEW ANY DATABASE` de nivel de servidor para ver la fila `DB_ID` correspondiente. Para la base de datos **master**, `DB_ID` necesita el permiso `CREATE DATABASE` como mínimo. La base de datos a la que se conecta el autor de la llamada siempre aparece en **sys.databases**.
  
> [!IMPORTANT]  
>  El rol público tiene el permiso `VIEW ANY DATABASE` de forma predeterminada, lo que permite a todos los inicios de sesión ver información de la base de datos. Para evitar que un inicio de sesión detecte una base de datos, use `REVOKE` para revocar el permiso `VIEW ANY DATABASE` del público, o bien use `DENY` para denegar el permiso `VIEW ANY DATABASE` para inicios de sesión individuales.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. Devolver el Id. de base de datos de la base de datos actual  
En este ejemplo se devuelve el identificador de base de datos de la base de datos actual.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. Devolver el Id. de base de datos de una base de datos específica  
En este ejemplo se devuelve el identificador de base de datos de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>C. Usar DB_ID para especificar el valor de un parámetro de una función del sistema  
En este ejemplo se usa `DB_ID` para devolver el identificador de base de datos de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en la función del sistema `sys.dm_db_index_operational_stats`. La función toma un Id. de base de datos como primer parámetro.
  
```sql
DECLARE @db_id int;  
DECLARE @object_id int;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
IF @db_id IS NULL   
  BEGIN;  
    PRINT N'Invalid database';  
  END;  
ELSE IF @object_id IS NULL  
  BEGIN;  
    PRINT N'Invalid object';  
  END;  
ELSE  
  BEGIN;  
    SELECT * FROM sys.dm_db_index_operational_stats(@db_id, @object_id, NULL, NULL);  
  END;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. Devolver el identificador de la base de datos actual  
En este ejemplo se devuelve el identificador de base de datos de la base de datos actual.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. Devolver el identificador de la base de datos con nombre  
En este ejemplo se devuelve el identificador de base de datos de la base de datos AdventureWorksDW2012.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>Vea también
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
[Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

