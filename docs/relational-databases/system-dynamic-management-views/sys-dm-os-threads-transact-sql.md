---
title: sys.dm_os_threads (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 740dcc22d53ff6cd60bbc491fb6bb7b7f44947a8
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577998"
---
# <a name="sysdmosthreads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una lista de todos los subprocesos del sistema operativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se están ejecutando en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_threads**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|Dirección de memoria (clave principal) del subproceso.|  
|started_by_sqlservr|**bit**|Indica el iniciador del subproceso.<br /><br /> 1 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inició el subproceso.<br /><br /> 0 = Otro componente inició el subproceso como un procedimiento almacenado extendido desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|os_thread_id|**int**|Identificador del subproceso asignado por el sistema operativo.|  
|status|**int**|Marca del estado interno|  
|instruction_address|**varbinary(8)**|Dirección de la instrucción que se está ejecutando en ese momento.|  
|creation_time|**datetime**|Hora a la que se creó este subproceso.|  
|kernel_time|**bigint**|Tiempo del kernel consumido por este subproceso.|  
|usermode_time|**bigint**|Tiempo de usuario consumido por este subproceso.|  
|stack_base_address|**varbinary(8)**|Dirección de memoria de la dirección de pila más alta de este subproceso.|  
|stack_end_address|**varbinary(8)**|Dirección de memoria de la dirección de pila más baja de este subproceso.|  
|stack_bytes_committed|**int**|Número de bytes confirmados en la pila.|  
|stack_bytes_used|**int**|Número de bytes que se usan de forma activa en el subproceso.|  
|affinity|**bigint**|Máscara de CPU en la que se ejecuta este subproceso. Esto depende del valor configurado por el **ALTER SERVER CONFIGURATION SET PROCESS AFFINITY** instrucción. Puede ser distinta del programador en caso de afinidad de software.|  
|Prioridad|**int**|Valor de prioridad de este subproceso.|  
|Configuración regional|**int**|LCID de la configuración regional en memoria caché del subproceso.|  
|Token|**varbinary(8)**|Identificador del token de suplantación en caché del subproceso.|  
|is_impersonating|**int**|Indica si este subproceso usa suplantación de Win32.<br /><br /> 1 = El subproceso usa credenciales de seguridad diferentes de las predeterminadas del proceso. Indica que el subproceso suplanta una entidad distinta de la que creó el proceso.|  
|is_waiting_on_loader_lock|**int**|Estado del sistema operativo que indica si el subproceso espera en el bloqueo de carga.|  
|fiber_data|**varbinary(8)**|Fibra actual de Win32 que se ejecuta en el subproceso. Esto solo se aplica cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para la agrupación ligera.|  
|thread_handle|**varbinary(8)**|Exclusivamente para uso interno.|  
|event_handle|**varbinary(8)**|Exclusivamente para uso interno.|  
|scheduler_address|**varbinary(8)**|Dirección de memoria del programador asociado con este subproceso. Para obtener más información, consulte [sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).|  
|worker_address|**varbinary(8)**|Dirección de memoria del trabajador enlazado a este subproceso. Para obtener más información, consulte [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).|  
|fiber_context_address|**varbinary(8)**|Dirección de contexto de fibra interna. Esto solo se aplica cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para la agrupación ligera.|  
|self_address|**varbinary(8)**|Puntero de comprobaciones de coherencia.|  
|processor_group|**smallint**|**Se aplica a**: desde [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador de grupo de procesadores.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="notes-on-linux-version"></a>Notas de la versión de Linux

Debido a cómo el motor de SQL funciona en Linux, parte de esta información no coincide con los datos de diagnóstico de Linux. Por ejemplo, `os_thread_id` no coincide con el resultado de herramientas como `ps`,`top` o el procfs (/ proc /`pid`).  Esto es debido a la capa de abstracción de plataforma (SQLPAL), una capa entre componentes de SQL Server y el sistema operativo.

## <a name="examples"></a>Ejemplos  
 Tras el inicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia subprocesos y después asocia trabajos a dichos subprocesos. Sin embargo, los componentes externos, como un procedimiento almacenado extendido, pueden iniciar subprocesos bajo el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no controla estos subprocesos. Sys.dm_os_threads puede proporcionar información sobre subprocesos rogue que consumen recursos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proceso.  
  
 La siguiente consulta se utiliza para buscar subprocesos de trabajo, junto con el tiempo consumido en la ejecución, que ejecutan subprocesos no iniciados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]
>  Por concisión, la siguiente consulta utiliza un asterisco (`*`) en la instrucción `SELECT`. Evite utilizar asteriscos (*), especialmente con vistas de catálogo, vistas de administración dinámica y funciones con valores de tabla del sistema. Las actualizaciones futuras y las versiones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede agregar columnas y cambiar el orden de columnas para estas funciones y vistas. Es posible que estos cambios provoquen errores en las aplicaciones que esperan un determinado orden y número de columnas.  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>Vea también  
  [sys.dm_os_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


