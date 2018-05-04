---
title: Sys.geo_replication_links (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/18/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9f36a6db31e498fc6bce6dc9da13bac88d3b3189
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>Sys.geo_replication_links (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Contiene una fila para cada vínculo de replicación entre bases de datos principales y secundarias de un perfil de replicación geográfica. Esta vista se encuentra en la base de datos maestra lógica.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Id. de la base de datos actual en la vista sys.databases.|  
|start_date|**datetimeoffset**|Hora UTC en un centro de datos regional de base de datos SQL cuando se inició la replicación de base de datos|  
|modify_date|**datetimeoffset**|Hora UTC en la base de datos SQL centro de datos regional cuando se haya completado la replicación geográfica de base de datos. La nueva base de datos está sincronizada con la base de datos principal en este momento. .|  
|link_guid|**uniqueidentifier**|Identificador único del vínculo de replicación geográfica.|  
|partner_server|**sysname**|Nombre del servidor lógico que contiene la base de datos de replicación geográfica.|  
|partner_database|**sysname**|Nombre de la base de datos de replicación geográfica en el servidor lógico vinculado.|  
|replication_state|**tinyint**|El estado de replicación geográfica para esta base de datos, uno de:.<br /><br /> 0 = pendiente. Creación de la base de datos secundaria activa está programada pero los pasos de preparación necesarios aún no están completos.<br /><br /> 1 = el inicio. El destino de replicación geográfica se está propagando pero las dos bases de datos no se ha sincronizado. Hasta que se complete la propagación, no se puede conectar a la base de datos secundaria. Quitar la base de datos secundaria desde el servidor principal se cancelará la operación de inicialización.<br /><br /> 2 = puesta al día. La base de datos secundaria está en un estado transaccionalmente coherente y se está sincronizando constantemente con la base de datos principal.|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|rol|**tinyint**|Rol de replicación geográfica, uno de:<br /><br /> 0 = primary. El database_id hace referencia a la base de datos principal de la asociación de replicación geográfica.<br /><br /> 1 = la base de datos secundaria.  El database_id hace referencia a la base de datos principal de la asociación de replicación geográfica.|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|El tipo secundario, uno de:<br /><br /> 0 = No. La base de datos secundaria no es accesible hasta que la conmutación por error.<br /><br /> 1 = ReadOnly. La base de datos secundaria solo es accesible para las conexiones de cliente con ApplicationIntent = ReadOnly.<br /><br /> 2 = Todas. La base de datos secundaria es accesible para cualquier conexión de cliente.|  
|secondary_allow_connections _desc|**nvarchar(256)**|no<br /><br /> Todos<br /><br /> Sólo lectura|  
  
## <a name="permissions"></a>Permissions  
 Esta vista solo está disponible en la **maestro** base de datos para el inicio de sesión de entidad de seguridad de nivel de servidor.  
  
## <a name="example"></a>Ejemplo  
 Mostrar todas las bases de datos con vínculos de replicación geográfica.  
  
```  
SELECT   
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc   
FROM sys.geo_replication_links;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [Sys.dm_geo_replication_link_status &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [Sys.dm_operation_status &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
