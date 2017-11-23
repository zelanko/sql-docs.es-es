---
title: Db_id (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_ID_TSQL
- DB_ID
dev_langs: TSQL
helpviewer_keywords:
- viewing database ID numbers
- IDs [SQL Server], databases
- database IDs [SQL Server]
- identification numbers [SQL Server], databases
- displaying database ID numbers
- DB_ID function
ms.assetid: 7b3aef89-a6fd-4144-b468-bf87ebf381b8
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 152e471cf63efa09b0fc6dcb65acd28a191699b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="dbid-transact-sql"></a>DB_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el número de identificación (identificador) de la base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DB_ID ( [ 'database_name' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
'*database_name*'  
Es el nombre de base de datos que se utiliza para devolver el Id. de base de datos correspondiente. *database_name* es **sysname**. Si *database_name* es se omite, se devuelve el identificador de base de datos actual.
  
## <a name="return-types"></a>Tipos de valor devuelto
**int**
  
## <a name="permissions"></a>Permissions  
Si el autor de llamada de **DB_ID** no es el propietario de la base de datos y la base de datos no es **maestro** o **tempdb**, los permisos mínimos necesarios para ver la fila correspondiente son Permiso de nivel de servidor ALTER ANY DATABASE o VIEW ANY DATABASE o permiso CREATE DATABASE en la **maestro** base de datos. La base de datos a la que está conectado el autor de la llamada siempre se puede ver en **sys.databases**.
  
> [!IMPORTANT]  
>  De forma predeterminada, la función public tiene el permiso VIEW ANY DATABASE, lo que permite todos los inicios de sesión ver información de la base de datos. Para bloquear un inicio de sesión de la capacidad para detectar una base de datos, REVOCAR el permiso VIEW ANY DATABASE de pública o denegar el permiso VIEW ANY DATABASE para inicios de sesión individuales.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-database-id-of-the-current-database"></a>A. Devolver el Id. de base de datos de la base de datos actual  
El siguiente ejemplo devuelve el Id. de base de datos de la base de datos actual.
  
```sql
SELECT DB_ID() AS [Database ID];  
GO  
```  
  
### <a name="b-returning-the-database-id-of-a-specified-database"></a>B. Devolver el Id. de base de datos de una base de datos específica  
En el ejemplo siguiente se devuelve el identificador de base de datos de la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos.
  
```sql
SELECT DB_ID(N'AdventureWorks2008R2') AS [Database ID];  
GO  
```  
  
### <a name="c-using-dbid-to-specify-the-value-of-a-system-function-parameter"></a>C. Usar DB_ID para especificar el valor de un parámetro de una función del sistema  
En el ejemplo siguiente se utiliza `DB_ID` para devolver el identificador de base de datos de la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos en la función del sistema `sys.dm_db_index_operational_stats`. La función toma un Id. de base de datos como primer parámetro.
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-return-the-id-of-the-current-database"></a>D. Devuelve el identificador de la base de datos actual  
El siguiente ejemplo devuelve el Id. de base de datos de la base de datos actual.
  
```sql
SELECT DB_ID();  
```  
  
### <a name="e-return-the-id-of-a-named-database"></a>E. Devuelve el identificador de una base de datos con nombre.  
En el ejemplo siguiente se devuelve el identificador de base de datos de la base de datos AdventureWorksDW2012.
  
```sql
SELECT DB_ID('AdventureWorksPDW2012');  
```  
  
## <a name="see-also"></a>Vea también
[Db_name &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
[Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)
  
  

