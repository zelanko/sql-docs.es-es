---
title: sys.sp_xtp_control_query_exec_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_query_exec_stats_TSQL
- sys.sp_xtp_control_query_exec_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_control_query_exec_stats
ms.assetid: 4838125d-ad1e-479e-b7d2-42655e8f4f02
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 86ab826d23f50868259edc5ae3b2bffa55359ce2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysspxtpcontrolqueryexecstats-transact-sql"></a>sys.sp_xtp_control_query_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Habilita la recopilación de estadísticas por consulta para todos los procedimientos almacenados compilados de forma nativa para la instancia y otros específicos.  
  
 El rendimiento disminuye cuando se habilita la recopilación de estadísticas. Si solo necesita solucionar los problemas de algunos procedimientos almacenados compilados de forma nativa, puede habilitar la recopilación de estadísticas únicamente para dichos procedimientos almacenados.  
  
 Para habilitar la recopilación de estadísticas en el nivel de procedimiento para todos los procedimientos almacenados compilados de forma nativa, vea [sys.sp_xtp_control_proc_exec_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_xtp_control_query_exec_stats [ [ @new_collection_value = ] collection_value ],  
[ [ @database_id = ] database_id   
[ , [ @xtp_object_id = ] procedure_id ] ,   
[ @old_collection_value] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 @new_collection_value= *valor*  
 Determina si la recopilación de estadísticas del nivel de procedimiento está activada (1) o desactivada (0).  
  
 @new_collection_valuese establece en cero cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia.  
  
 @database_id = = *database_id*, @xtp_object_id = *procedure_id*  
 El identificador de la base de datos y el identificador de objeto para el procedimiento almacenado compilado de forma nativa. Si está habilitada la recopilación de estadísticas para la instancia ([sys.sp_xtp_control_proc_exec_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md)), se recopilan estadísticas para un procedimiento almacenado compilado de forma nativa. Al desactivar la recopilación de estadísticas en la instancia, no se desactiva la recopilación de estadísticas para procedimientos almacenados compilados de forma nativa individuales.  
  
 Use [sys.databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md), [sys.procedures &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md), [DB_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/db-id-transact-sql.md), o [OBJECT_ID &#40; Transact-SQL &#41; ](../../t-sql/functions/object-id-transact-sql.md) obtener identificadores de una base de datos y el procedimiento almacenado.  
  
 @old_collection_value= *valor*  
 Devuelve el estado actual.  
  
## <a name="return-code"></a>Código de retorno  
 0 para correcto. Distinto de cero para error.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de sysadmin.  
  
## <a name="code-sample"></a>Ejemplo de código  
 En el siguiente ejemplo de código se muestra cómo habilitar la recopilación de estadísticas para todos los procedimientos almacenados compilados de forma nativa para la instancia y, a continuación, para uno específico.  
  
```sql   
DECLARE @c bit  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1;  
  
EXEC sp_xtp_control_query_exec_stats @old_collection_value=@c output;  
SELECT @c AS 'collection status';  
  
EXEC [sys].[sp_xtp_control_query_exec_stats] @new_collection_value = 1,   
@database_id = 5, @xtp_object_id = 341576255;  
  
EXEC sp_xtp_control_query_exec_stats @database_id = 5,   
@xtp_object_id = 341576255, @old_collection_value=@c output;  
  
SELECT @c AS 'collection status';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
