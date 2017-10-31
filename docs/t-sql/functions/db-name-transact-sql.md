---
title: Db_name (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5743ccb1374640078a77d84a140e9e5d0fdaef0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el nombre de la base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*database_id*  
Es el número de identificación (Id.) de la base de datos que se va a devolver. *database_id* es **int**, no tiene ningún valor predeterminado. Si no se especifica el Id., se devuelve el nombre de la base de datos actual.
  
## <a name="return-types"></a>Tipos de valor devuelto
**nvarchar (128)**
  
## <a name="permissions"></a>Permissions  
Si el autor de llamada de **DB_NAME** no es el propietario de la base de datos y la base de datos no es **maestro** o **tempdb**, los permisos mínimos necesarios para ver la fila correspondiente son Permiso de nivel de servidor ALTER ANY DATABASE o VIEW ANY DATABASE o permiso CREATE DATABASE en la **maestro** base de datos. La base de datos a la que está conectado el autor de la llamada siempre se puede ver en **sys.databases**.
  
> [!IMPORTANT]  
>  De forma predeterminada, la función public tiene el permiso VIEW ANY DATABASE, lo que permite todos los inicios de sesión ver información de la base de datos. Para bloquear un inicio de sesión de la capacidad para detectar una base de datos, REVOCAR el permiso VIEW ANY DATABASE de pública o denegar el permiso VIEW ANY DATABASE para inicios de sesión individuales.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-current-database-name"></a>A. Devolver el nombre de la base de datos actual  
En el ejemplo siguiente se devuelve el nombre de la base de datos actual.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. Devolver el nombre de la base de datos de un identificador de base de datos específico  
En el ejemplo siguiente se devuelve el nombre de la base de datos con Id. `3`.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. Devolver el nombre de base de datos actual  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Devolver el nombre de una base de datos utilizando el identificador de base de datos  
En el ejemplo siguiente se devuelve el nombre de base de datos y database_id para cada base de datos.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Vea también
[Db_id &#40; Transact-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  


