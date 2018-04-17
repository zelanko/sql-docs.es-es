---
title: Sys.dm_os_cluster_nodes (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes_TSQL
- dm_os_cluster_nodes
- sys.dm_os_cluster_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_cluster_nodes dynamic management view
ms.assetid: 92fa804e-2d08-42c6-a36f-9791544b1d42
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3da465e5ebe38965f81af83473ff1b1b6c9dbf68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosclusternodes-transact-sql"></a>sys.dm_os_cluster_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada nodo en la configuración de la instancia en clúster de conmutación por error. Si la instancia actual es una instancia en clúster de conmutación por error, devuelve una lista de nodos en los que se ha definido esta instancia en clúster de conmutación por error (antes "servidor virtual"). Si la instancia del servidor actual no es una instancia en clúster de conmutación por error, devuelve un conjunto de filas vacío.  
  
> **Nota:** para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_cluster_nodes**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**nodeName**|**sysname**|Nombre de un nodo en la configuración de la instancia en clúster de conmutación por error (servidor virtual) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|status|**int**|Estado del nodo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error: 0, 1, 2, 3, -1. Para obtener más información, consulte [GetClusterNodeState Function](http://go.microsoft.com/fwlink/?LinkId=204794).|  
|status_description|**nvarchar (20)**|Descripción del estado del nodo de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0: activo<br /><br /> 1: inactivo<br /><br /> 2: en pausa<br /><br /> 3: uniéndose<br /><br /> -1 = desconocido|  
|is_current_owner|bit|1 significa que este nodo es el propietario actual del recurso de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="remarks"></a>Comentarios  
 Si se habilita la agrupación en clústeres de conmutación por error, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede ejecutar en cualquiera de los nodos del clúster de conmutación por error designados como parte de la configuración de la instancia en clúster de conmutación por error (servidor virtual) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> **Nota:** esta vista reemplaza la función fn_virtualservernodes, que dejará de utilizarse en una versión futura.  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso VIEW SERVER STATE en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa sys. dm_os_cluster_nodes para devolver los nodos de una instancia de servidor en clúster.  
  
```  
SELECT NodeName, status, status_description, is_current_owner   
FROM sys.dm_os_cluster_nodes;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|NodeName|status|status_description|is_current_owner|  
|--------------|------------|-------------------------|------------------------|  
|node1|0|up|1|  
|node2|0|up|0|  
|Nodo3|1|down|0|  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_os_cluster_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-properties-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [Sys.fn_virtualservernodes &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  



