---
title: Sys.dm_database_copies (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9b2e5b7b257ea0a22cf847f4e28f58c3c89a2d68
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdatabasecopies-azure-sql-database"></a>sys.dm_database_copies (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de la copia de la base de datos.  
  
Para obtener información acerca de los vínculos de replicación geográfica, use la [sys.geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md) o [sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) vistas (disponibles en la base de datos SQL V12).
  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|El identificador de la base de datos actual en la vista `sys.databases`.|  
|**start_date**|**datetimeoffset**|La hora UTC en un centro de datos regional de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] a la que se inició la copia de la base de datos.|  
|**modify_date**|**datetimeoffset**|La hora UTC en un centro de datos regional de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] a la que se ha completado la copia de la base de datos. La nueva base de datos es transaccionalmente coherente con la base de datos principal en este momento. La información de finalización se actualiza cada minuto.<br /><br />Hora UTC que refleja la última actualización del campo percent_complete.|  
|**percent_complete**|**real**|Porcentaje de bytes que se han copiado. Los valores pueden oscilar entre 0 y 100. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] puede recuperarse automáticamente de algunos errores, como la conmutación por error, y reiniciar la copia de la base de datos. En este caso, percent_complete se reiniciaría desde 0.|  
|**error_code**|**int**|Cuando es mayor que 0, el código que indica el error que ha aparecido mientras se realizaba la copia. El valor es igual a 0 si no se ha producido ningún error.|  
|**error_desc**|**nvarchar(4096)**|Descripción del error que se produjo durante la copia.|  
|**error_severity**|**int**|Devuelve 16 si se produjo un error en la copia de la base de datos.|  
|**error_state**|**int**|Devuelve 1 si se produjo un error en la copia.|  
|**copy_guid**|**uniqueidentifier**|Identificador único de la operación de copia.|  
|**partner_server**|**sysname**|Nombre del servidor de base de datos SQL donde se crea la copia.|  
|**partner_database**|**sysname**|Nombre de la copia de la base de datos en el servidor asociado.|  
|**replication_state**|**tinyint**|El estado de replicación de copia continua para esta base de datos. Los valores son:<br /><br /> 0 = pendiente. Creación de la copia de la base de datos está programada pero los pasos de preparación necesarios aún no están completos o han sido bloqueados temporalmente por la cuota de propagación.<br /><br /> 1 = el inicio. La base de datos de copia está propagando no está aún totalmente sincronizado con la base de datos de origen. En este estado no se puede conectar a la copia. Para cancelar la operación de inicialización en curso, se debe quitar la base de datos de copia.|  
|**replication_state_desc**|**nvarchar(256)**|Descripción del estado de replication_state, uno de los siguientes:<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**int**|Campo reservado.|  
|**is_continuous_copy**|**bit**|0 = devuelve 0|  
|**is_target_role**|**bit**|0 = base de datos de origen<br /><br /> 1 = la base de datos de copia|  
|**is_interlink_connected**|bit|Campo reservado.|  
|**is_offline_secondary**|bit|Campo reservado.|  
  
## <a name="permissions"></a>Permissions  
 Esta vista solo está disponible en la **maestro** base de datos para el inicio de sesión de entidad de seguridad de nivel de servidor.  
  
## <a name="remarks"></a>Comentarios  
 Puede usar el **sys.dm_database_copies** ver en el **maestro** base de datos de origen o destino [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server. Cuando la copia de la base de datos se completa correctamente y la nueva base de datos tenga el estado ONLINE, la fila en la **sys.dm_database_copies** vista se quita automáticamente.  
  
  
