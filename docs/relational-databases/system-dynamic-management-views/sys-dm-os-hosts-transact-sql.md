---
title: Sys. dm_os_hosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3e3d49d77dbee94bb365d58b7012c45cdaddf4f7
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898797"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve todos los host registrados actualmente en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta vista también devuelve los recursos utilizados por estos host.  
  
> [!NOTE]  
>  Para llamar a este método desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use el nombre **Sys. dm_pdw_nodes_os_hosts**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8**|Dirección de memoria interna del objeto host.|  
|**type**|**nvarchar(60)**|Tipo de componente hospedado. Por ejemplo,<br /><br /> SOSHOST_CLIENTID_SERVERSNI= Interfaz de SQL Server Native<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = Proveedor OLE DB de SQL Server Native Client<br /><br /> SOSHOST_CLIENTID_MSDART = Tiempo de ejecución de Microsoft Data Access|  
|**name**|**nvarchar(32)**|Nombre del host.|  
|**enqueued_tasks_count**|**int**|Número total de tareas que este host ha colocado en colas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**active_tasks_count**|**int**|Número de tareas actualmente en ejecución que este host ha colocado en colas.|  
|**completed_ios_count**|**int**|Número total de E/S emitidas y completadas mediante este host.|  
|**completed_ios_in_bytes**|**bigint**|Recuento total de bytes de E/S completadas mediante este host.|  
|**active_ios_count**|**int**|Número total de solicitudes de E/S relacionadas con este host que esperan actualmente a completarse.|  
|**default_memory_clerk_address**|**varbinary(8**|Dirección de memoria del objeto del distribuidor de memoria asociado a este host. Para obtener más información, vea [Sys. dm_os_memory_clerks &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Identificador del nodo en el que se encuentra esta distribución.|  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requiere el `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles Premium, requiere el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] los niveles estándar y básico, requiere el **Administrador del servidor** o una cuenta de **Administrador de Azure Active Directory** .   

## <a name="remarks"></a>Comentarios  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite componentes, como un proveedor OLE DB, que no forman parte del ejecutable de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para asignar memoria y participar en la programación no preferente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospeda estos componentes y se realiza un seguimiento de todos los recursos asignados por ellos. El hospedaje permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contar mejor con los recursos usados por componentes externos al ejecutable de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|uno a uno|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|uno a uno|  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se determina la cantidad total de memoria confirmada por un componente hospedado.  
  
||  
|-|  
|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>Consulte también  

 [Sys. dm_os_memory_clerks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [SQL Server vistas de administración dinámica relacionadas con el sistema operativo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


