---
title: sp_dbremove (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbremove
- sp_dbremove_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbremove
ms.assetid: a8513f4a-c025-49c8-99c3-4c83cb7f51ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b801980f6a9f7bc2fc434a9fac19e204bbc60cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655903"
---
# <a name="spdbremove-transact-sql"></a>sp_dbremove (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una base de datos y todos los archivos asociados con ella.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Se recomienda que use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbremove [ @dbname = ] 'database' [ , [ @dropdev = ] 'dropdev' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=** ] **'***base de datos***'**  
 Es el nombre de la base de datos que se va a quitar. *base de datos* es **sysname**, su valor predeterminado es null.  
  
 [  **@dropdev=** ] **'***dropdev***'**  
 Es una marca proporcionada solo para garantizar la compatibilidad con versiones anteriores y actualmente se omite. *dropdev* tiene el valor **dropdev**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita una base de datos denominada `sales` y todos los archivos asociados con ella.  
  
```  
EXEC sp_dbremove sales;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
  
