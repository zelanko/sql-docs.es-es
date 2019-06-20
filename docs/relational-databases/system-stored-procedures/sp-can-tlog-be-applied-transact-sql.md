---
title: sp_can_tlog_be_applied (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_can_tlog_be_applied_TSQL
- sp_can_tlog_be_applied
dev_langs:
- TSQL
helpviewer_keywords:
- sp_can_tlog_be_applied
ms.assetid: 9c143b6c-27ac-4ab7-98d1-3b7b265f3963
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d21de1f416344202911f80e48afc025cd423b1e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62995456"
---
# <a name="spcantlogbeapplied-transact-sql"></a>sp_can_tlog_be_applied (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comprueba si una copia de seguridad del registro de transacciones se puede aplicar a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. **sp_can_tlog_be_applied** requiere que la base de datos esté en estado Restoring.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_can_tlog_be_applied [ @backup_file_name = ] 'backup_file_name'   
        , [ @database_name = ] 'database_name'   
        , [ @result = ] result OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @backup_file_name = ] 'backup_file_name'` Es el nombre de un archivo de copia de seguridad. *nombreDelArchivoDeCopiaDeSeguridad* es **nvarchar (128)** .  
  
`[ @database_name = ] 'database_name'` Es el nombre de la base de datos. *database_name* es **sysname**.  
  
`[ @result = ] _result_ OUTPUT` Indica si el registro de transacciones se puede aplicar a la base de datos. *resultado* es **bits**.  
  
 1 = El registro se puede aplicar.  
  
 0 = El registro no se puede aplicar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_can_tlog_be_applied**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se declara una variable local, `@MyBitVar`, para almacenar el resultado.  
  
```  
USE master;  
GO  
DECLARE @MyBitVar BIT;  
EXEC sp_can_tlog_be_applied  
     @backup_file_name =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\AdventureWorks2012.bak',  
     @database_name = N'AdventureWorks2012',  
     @result = @MyBitVar OUTPUT;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
