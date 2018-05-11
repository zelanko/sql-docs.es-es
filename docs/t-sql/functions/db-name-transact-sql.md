---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
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
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1c2a2e92fdef5cae1b2404d18c2c5fb18b3de1ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el nombre de la base de datos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*database_id*  
Es el número de identificación (Id.) de la base de datos que se va a devolver. *database_id* es de tipo **int** y no tiene ningún valor predeterminado. Si no se especifica el Id., se devuelve el nombre de la base de datos actual.
  
## <a name="return-types"></a>Tipos de valores devueltos
**nvarchar(128)**
  
## <a name="permissions"></a>Permisos  
Si el autor de la llamada de **DB_NAME** no es el propietario de la base de datos y la base de datos no es **maestra** o **tempdb**, los permisos mínimos necesarios para ver la fila correspondiente son el permiso ALTER ANY DATABASE o VIEW ANY DATABASE de nivel de servidor, o el permiso CREATE DATABASE en la base de datos **maestra**. La base de datos a la que está conectado el autor de la llamada siempre se puede ver en **sys.databases**.
  
> [!IMPORTANT]  
>  El rol público tiene el permiso VIEW ANY DATABASE de forma predeterminada, lo que permite a todos los inicios de sesión ver información de la base de datos. Para impedir que un inicio de sesión tenga capacidad para detectar una base de datos, revoque el permiso VIEW ANY DATABASE del rol público o deniegue el permiso VIEW ANY DATABASE a inicios de sesión individuales.  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. Devolver el nombre de la base de datos actual  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. Devolver el nombre de la base de datos usando el identificador de base de datos  
En el siguiente ejemplo se devuelve el nombre y el identificador de base de datos de cada base de datos.
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>Vea también
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[Funciones de metadatos &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

