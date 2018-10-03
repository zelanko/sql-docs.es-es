---
title: Sys.dm_hadr_cluster_members (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_cluster_members_TSQL
- sys.dm_hadr_cluster_members
- dm_hadr_cluster_members_TSQL
- dm_hadr_cluster_members
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], WSFC clusters
- sys.dm_hadr_cluster_members catalog view
ms.assetid: feb20b3a-8835-41d3-9a1c-91d3117bc170
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71493b066385840d065ff51e1f202c547686f774
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47857117"
---
# <a name="sysdmhadrclustermembers-transact-sql"></a>sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Si el nodo de WSFC que hospeda una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitada para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] tiene quórum de WSFC, devuelve una fila para cada uno de los miembros que constituyen el quórum y el estado de cada uno de ellos. Esto incluye todos los nodos del clúster (devueltos con el tipo CLUSTER_ENUM_NODE por la **Clusterenum** función) y el testigo de disco o recurso compartido de archivos, si existe. La fila devuelta para un miembro determinado contiene información sobre el estado de ese miembro. Por ejemplo, para un clúster de cinco nodos con quórum de mayoría de nodo en el que un nodo está inactivo, cuando **sys.dm_hadr_cluster_members** se consultan desde una instancia del servidor que está habilitado para [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] que reside en un nodo con quórum, **sys.dm_hadr_cluster_members** refleja el estado del nodo inactivo como "NODE_DOWN".  
  
 Si el nodo de WSFC no tiene el quórum, no se devuelve ninguna fila.  
  
 Use esta vista de administración dinámica para responder las preguntas siguientes:  
  
-   ¿Qué nodos se están ejecutando actualmente en el clúster de WSFC?  
  
-   ¿Cuántos errores más puede tolerar el clúster de WSFC antes de perder el quórum en un caso de mayoría de nodo?  

 > [!TIP]
 > A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], esta vista de administración dinámica admite siempre en Failover Cluster Instances además de grupos de disponibilidad AlwaysOn.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**MEMBER_NAME**|**nvarchar(128)**|Nombre de miembro, que puede ser un nombre de equipo, una letra de unidad o una ruta de acceso de recurso compartido de archivos.|  
|**MEMBER_TYPE**|**tinyint**|Tipo del miembro; puede ser:<br /><br /> 0 = Nodo de WSFC<br /><br /> 1 = Testigo de disco<br /><br /> 2 = Testigo de recurso compartido de archivos|  
|**member_type_desc**|**nvarchar(50)**|Descripción de **member_type**, uno de:<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS|  
|**member_state**|**tinyint**|El estado del miembro; puede ser:<br /><br /> 0 = Sin conexión<br /><br /> 1 = En línea|  
|**member_state_desc**|**nvarchar(60)**|Descripción de **member_state**, uno de:<br /><br /> UP<br /><br /> ABAJO|  
|**number_of_quorum_votes**|**tinyint**|Número de votos de quórum propiedad de este miembro de quórum. En el caso de que no haya mayoría: quórums de Solo disco: el valor predeterminado de este valor es 0. Para otros tipos de quórum, el valor predeterminado de este valor es 1.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
