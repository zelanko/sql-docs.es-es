---
title: sys.fn_trace_getfilterinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_trace_getfilterinfo
- fn_trace_getfilterinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], filters
- sys.fn_trace_getfilterinfo function
- filters [SQL Server], traces
- fn_trace_getfilterinfo function
ms.assetid: 09fe4a28-ff8a-4655-9da1-4654d5bc514d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1af9d4794d952e1ecb82e28a225e782039aff901
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sysfntracegetfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de los filtros que se aplicaron a un seguimiento determinado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use eventos extendidos en su lugar.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *trace_id*  
 Es el identificador de seguimiento. *trace_id* es **int**, no tiene ningún valor predeterminado.  
  
## <a name="tables-returned"></a>Tablas devueltas  
 Devuelve la siguiente información. Para obtener más información acerca de las columnas, vea [sp_trace_setfilter &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|Id. de la columna en la que se aplica el filtro.|  
|**logical_operator**|**int**|Especifica si se aplican los operadores AND u OR.|  
|**comparison_operator**|**int**|Especifica el tipo de comparación realizado:<br /><br /> 0 = Igual<br /><br /> 1 = No igual a<br /><br /> 2 = Mayor que<br /><br /> 3 = Menor que<br /><br /> 4 = Mayor o igual que<br /><br /> 5 = Menor o igual que<br /><br /> 6 = Como<br /><br /> 7 = No es como|  
|**value**|**sql_variant**|Especifica el valor sobre el que se aplica el filtro.|  
  
## <a name="remarks"></a>Comentarios  
 Los conjuntos de usuarios *trace_id* valor para identificar, modificar y controlar el seguimiento. Cuando se pasa el identificador de un seguimiento específico, **fn_trace_getfilterinfo** devuelve información acerca de cualquier filtro de seguimiento. Si el seguimiento especificado no tiene un filtro, esta función devuelve un conjunto de filas vacío. Si se pasa un Id. no válido, esta función devuelve un conjunto de filas vacío. Para obtener información similar acerca de los seguimientos, vea [sys.fn_trace_getinfo &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER TRACE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve información sobre todos los filtros del seguimiento número 2.  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear un seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
