---
title: DB_NAME (Transact-SQL) | Microsoft Docs
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 22905cbe658689fb5edcf4f4f984832ffc0429d3
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452829"
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve el nombre de una base de datos especificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*database_id*  

El número de identificación de la base de datos cuyo nombre va a devolver `DB_NAME`. Si la llamada a `DB_NAME` omite *database_id*, `DB_NAME` devuelve el nombre de la base de datos actual.
  
## <a name="return-types"></a>Tipos de valores devueltos
**nvarchar(128)**
  
## <a name="permissions"></a>Permisos  

Si el autor de la llamada de `DB_NAME` no posee una base de datos **master** o distinta de **tempdb** determinada, como mínimo se requieren los permisos `ALTER ANY DATABASE` o `VIEW ANY DATABASE` de nivel de servidor para ver la fila `DB_ID` correspondiente. Para la base de datos **master**, `DB_ID` necesita el permiso `CREATE DATABASE` como mínimo. La base de datos a la que se conecta el autor de la llamada siempre aparece en **sys.databases**.
  
> [!IMPORTANT]  
>  El rol público tiene el permiso `VIEW ANY DATABASE` de forma predeterminada, lo que permite a todos los inicios de sesión ver información de la base de datos. Para evitar que un inicio de sesión detecte una base de datos, use `REVOKE` para revocar el permiso `VIEW ANY DATABASE` del público, o bien use `DENY` para denegar el permiso `VIEW ANY DATABASE` para inicios de sesión individuales.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-current-database-name"></a>A. Devolver el nombre de la base de datos actual  
En este ejemplo se devuelve el nombre de la base de datos actual.
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. Devolver el nombre de la base de datos de un identificador de base de datos específico  
En este ejemplo se devuelve el nombre de la base de datos con el identificador `3`.
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. Devolver el nombre de la base de datos actual  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Devolver el nombre de la base de datos usando el identificador de base de datos  
En este ejemplo se devuelve el nombre y el identificador de base de datos de cada base de datos.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Vea también
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

