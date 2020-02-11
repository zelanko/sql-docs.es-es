---
title: Sys. dm_os_memory_brokers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
author: stevestein
ms.author: sstein
ms.openlocfilehash: a8e131e2550ffa5078df5e284898ffe936128b7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265873"
---
# <a name="sysdm_os_memory_brokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las asignaciones internas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizan el administrador de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El seguimiento de la diferencia entre los contadores de memoria de proceso de **Sys. dm_os_process_memory** y los contadores internos puede indicar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uso de memoria de componentes externos en el espacio de memoria.  
  
 Los agentes de memoria distribuyen equitativamente las asignaciones de memoria entre varios componentes dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en función del uso actual y previsto. Los agentes de memoria no realizan las asignaciones. Solo realizan el seguimiento de las asignaciones para calcular la distribución.  
  
 La tabla siguiente proporciona información sobre los agentes de memoria.  
  
> [!NOTE]  
>  Para llamar a este [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] método [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]desde o, use el nombre **Sys. dm_pdw_nodes_os_memory_brokers**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|Id. del grupo de recursos de servidor si está asociado a un grupo del regulador de recursos.|  
|**memory_broker_type**|**nvarchar (60)**|Tipo de agente de memoria. Actualmente hay tres tipos de agentes de memoria en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que se enumeran a continuación con sus descripciones.<br /><br /> **MEMORYBROKER_FOR_CACHE** : memoria asignada para su uso por parte de objetos almacenados en caché (no caché del grupo de búferes).<br /><br /> **MEMORYBROKER_FOR_STEAL** : memoria que se ha robado del grupo de búferes. Esta memoria no está disponible para ser reutilizada por otros componentes hasta que el propietario actual la libere.<br /><br /> **MEMORYBROKER_FOR_RESERVE** : memoria reservada para un uso futuro por parte de las solicitudes que se están ejecutando actualmente.|  
|**allocations_kb**|**BIGINT**|La cantidad de memoria, en kilobytes (KB) asignada a este tipo de agente.|  
|**allocations_kb_per_sec**|**BIGINT**|La tasa de asignaciones de memoria en kilobytes (KB) por segundo. Este valor puede ser negativo para las cancelaciones de asignación de memoria.|  
|**predicted_allocations_kb**|**BIGINT**|La cantidad prevista de memoria asignada por el agente. Depende del modelo de uso de la memoria.|  
|**target_allocations_kb**|**BIGINT**|La cantidad recomendada de memoria asignada, en kilobytes (KB), depende de la configuración actual y del modelo de uso de la memoria. El agente debería aumentar o disminuir hasta este número.|  
|**future_allocations_kb**|**BIGINT**|El número previsto de asignaciones, en kilobytes (KB), que se realizarán en los segundos siguientes.|  
|**overall_limit_kb**|**BIGINT**|Cantidad máxima de memoria, en kilobytes (KB), que el agente puede asignar.|  
|**last_notification**|**nvarchar (60)**|Recomendación del uso de memoria, que depende de la configuración actual y del modelo de uso. Los valores válidos son los siguientes:<br /><br /> grow<br /><br /> shrink<br /><br /> stable|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   
  
## <a name="see-also"></a>Consulte también  

  [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


