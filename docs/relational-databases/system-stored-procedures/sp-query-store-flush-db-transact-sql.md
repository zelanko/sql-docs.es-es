---
title: sp_query_store_flush_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_query_store_flush_db_TSQL
- sys.sp_query_store_flush_db_TSQL
- sp_query_store_flush_db
- sys.sp_query_store_flush_db
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_query_store_flush_db
- sp_query_store_flush_db
ms.assetid: 580c03ae-57fc-4562-a6bb-5ec89521e38c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 96c4e7a366c1235fa1062e5d66c2d6be160a6d22
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68418893"
---
# <a name="sp_query_store_flush_db-transact-sql"></a>sp_query_store_flush_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Vacía la parte en memoria de los Almacén de consultas datos en el disco.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_query_store_flush_db [;]  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **ALTER** en la base de datos.
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se vacía la parte en memoria de los datos de Almacén de consultas en el disco.  
  
```  
EXEC sp_query_store_flush_db;  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_query_store_force_plan &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)   
 [sp_query_store_remove_query &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-remove-query-transact-sql.md)   
 [sp_query_store_unforce_plan &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)   
 [sp_query_store_reset_exec_stats &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [sp_query_store_remove_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-remove-plan-transct-sql.md)   
 [sp_query_store_reset_exec_stats &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-query-store-reset-exec-stats-transact-sql.md)   
 [Almacén de consultas vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [Supervisar el rendimiento mediante el Almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
  
  
