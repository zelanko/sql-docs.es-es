---
title: sp_trace_setstatus (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b71e79f28abb5932fc9a7a644bf466f848c1e6e7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534807"
---
# <a name="sptracesetstatus-transact-sql"></a>sp_trace_setstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica el estado actual del seguimiento especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use eventos extendidos en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @traceid = ] trace_id` Es el identificador del objeto trace que se puede modificar. *trace_id* es **int**, no tiene ningún valor predeterminado. El usuario utiliza este *trace_id* valor para identificar, modificar y controlar el seguimiento. Para obtener información acerca de cómo recuperar el *trace_id*, consulte [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
`[ @status = ] status` Especifica la acción que se implementará en el seguimiento. *estado* es **int**, no tiene ningún valor predeterminado.  
  
 En la tabla siguiente se muestra una lista de los estados que podrían especificarse.  
  
|Estado|Descripción|  
|------------|-----------------|  
|**0**|Detiene el seguimiento especificado.|  
|**1**|Inicia el seguimiento especificado.|  
|**2**|Cierra el seguimiento especificado y elimina su definición del servidor.|  
  
> [!NOTE]  
>  Para poder cerrar un seguimiento, primero debe detenerse. Para poder ver un seguimiento, antes debe detenerse y cerrarse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 En la tabla siguiente se describen los valores del código que los usuarios pueden obtener después de completar el procedimiento almacenado.  
  
|Código de retorno|Descripción|  
|-----------------|-----------------|  
|**0**|Ningún error.|  
|**1**|Error desconocido.|  
|**8**|El estado especificado no es válido.|  
|**9**|El controlador de traza especificado no es válido.|  
|**13**|Memoria insuficiente. Se devuelve cuando no hay memoria suficiente para realizar la acción especificada.|  
  
 Si el seguimiento ya está en el estado especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá **0**.  
  
## <a name="remarks"></a>Comentarios  
 Los parámetros de seguimiento de SQL de todos los procedimientos almacenados (**sp_trace_xx**) deben escribirse. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
 Para obtener un ejemplo de cómo usar los procedimientos almacenados de seguimiento, vea [Crear un seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 El usuario debe tener permiso ALTER TRACE.  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
