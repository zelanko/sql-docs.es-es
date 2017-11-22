---
title: DBCC FREESESSIONCACHE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREESESSIONCACHE
- FREESESSIONCACHE_TSQL
- DBCC_FREESESSIONCACHE_TSQL
- DBCC FREESESSIONCACHE
dev_langs: TSQL
helpviewer_keywords:
- DBCC FREESESSIONCACHE statement
- distributed queries [SQL Server], cache
- clearing distributed query cache
- flushing distributed query cache
ms.assetid: a256ba63-7e11-4d5e-abc0-1fa4ed072e63
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 48066cc155c3cfa507c35c4e10b8f129e3338363
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-freesessioncache-transact-sql"></a>DBCC FREESESSIONCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Vaciados de la caché de conexión de consulta distribuida utilizada por las consultas distribuidas en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
```sql
DBCC FREESESSIONCACHE [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se vacía la caché de la consulta distribuida.
  
```sql
USE AdventureWorks2012;  
GO  
DBCC FREESESSIONCACHE WITH NO_INFOMSGS;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
