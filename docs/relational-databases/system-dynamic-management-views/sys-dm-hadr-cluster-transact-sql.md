---
title: Sys.dm_hadr_cluster (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
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
- sys.dm_hadr_cluster
- dm_hadr_cluster_HADR
- sys.dm_hadr_cluster_TSQL
- dm_hadr_cluster
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: 13ce70e4-9d43-4a80-a826-099e6213bf85
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 911630f4d93505611d3773f61b8afc5f1a4d9dda
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmhadrcluster-transact-sql"></a>sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Si el nodo de clústeres de conmutación por error de servidor de Windows (WSFC) que hospeda una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tiene quórum de WSFC, **sys.dm_hadr_cluster** devuelve una fila que expone el nombre del clúster e información acerca del quórum. Si el nodo de WSFC no tiene quórum, no se devuelve ninguna fila.  
 > [!TIP]
 > A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], esta vista de administración dinámica admite siempre en Failover Cluster Instances además de grupos de disponibilidad AlwaysOn.

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|Nombre de clúster de WSFC que hospeda las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilitadas para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**quorum_type**|**tinyint**|Tipo de quórum utilizado por este clúster de WSFC; puede ser:<br /><br /> 0 = Mayoría de nodo. Esta configuración de quórum puede admitir errores de la mitad de los (con redondeo por exceso) menos uno. Por ejemplo, en un clúster de siete nodos, esta configuración de quórum puede admitir errores de tres nodos.<br /><br /> 1 = Nodo y mayoría de disco. Si el testigo de disco permanece en línea, esta configuración de quórum puede admitir errores de la mitad del número de nodos (con redondeo por exceso). Por ejemplo, un clúster de seis nodos en el que el testigo de disco está en línea puede admitir errores de tres nodos. Si el testigo de disco se queda sin conexión o sufre un error, esta configuración de quórum puede admitir errores de la mitad de los nodos (con redondeo por exceso) menos uno. Por ejemplo, un clúster de seis nodos con un testigo de disco con errores puede admitir errores de 3-1=2 nodos.<br /><br /> 2 = Nodo y mayoría de recurso compartido de archivos. Esta configuración de quórum funciona de forma similar a Nodo y mayoría del disco, pero utiliza un testigo de recurso compartido de archivos en lugar de un testigo de disco.<br /><br /> 3 = Sin mayoría: solo disco. Si el disco de quórum está en línea, esta configuración de quórum puede admitir errores de todos los nodos excepto uno.|  
|**quorum_type_desc**|**varchar(50)**|Descripción de **quorum_type**, uno de:<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY: _DISK_ONLY|  
|**quorum_state**|**tinyint**|Estado del quórum de WSFC, uno de los siguientes:<br /><br /> 0 = estado de quórum desconocido<br /><br /> 1 = Quórum normal<br /><br /> 2 = Quórum forzado|  
|**quorum_state_desc**|**varchar(50)**|Descripción de **quorum_state**, uno de:<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Supervisar grupos de disponibilidad & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
