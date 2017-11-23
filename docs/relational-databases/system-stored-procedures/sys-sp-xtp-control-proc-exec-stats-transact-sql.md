---
title: Sys.sp_xtp_control_proc_exec_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_control_proc_exec_stats
- sys.sp_xtp_control_proc_exec_stats_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_control_proc_exec_stats
ms.assetid: f5119808-76a1-4522-8529-9e02ee39adcb
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 721c120c200bb3142b36e06beb6e45cab1ca0805
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpcontrolprocexecstats-transact-sql"></a>sys.sp_xtp_control_proc_exec_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Habilita la recopilación de estadísticas para los procedimientos almacenados compilados de forma nativa.  
  
 Para habilitar la recopilación de estadísticas en el nivel de consulta para los procedimientos almacenados compilados de forma nativa, vea [sys.sp_xtp_control_query_exec_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_xtp_control_proc_exec_stats [ [ @new_collection_value = ] collection_value ], [ @old_collection_value]  
```  
  
## <a name="arguments"></a>Argumentos  
 @new_collection_value= *valor*  
 Determina si la recopilación de estadísticas del nivel de procedimiento está activada (1) o desactivada (0).  
  
 @new_collection_valuese establece en cero cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o inicia la base de datos.  
  
 @old_collection_value= *valor*  
 Devuelve el estado actual.  
  
## <a name="return-code"></a>Código de retorno  
 0 para correcto. Distinto de cero para error.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de sysadmin.  
  
## <a name="code-samples"></a>Ejemplos de código  
 Para establecer @new_collection_value y la consulta para el valor de@new_collection_value:  
  
```  
exec [sys].[sp_xtp_control_proc_exec_stats] @new_collection_value = 1  
declare @c bit  
exec sp_xtp_control_proc_exec_stats @old_collection_value=@c output  
select @c as 'collection status'  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
