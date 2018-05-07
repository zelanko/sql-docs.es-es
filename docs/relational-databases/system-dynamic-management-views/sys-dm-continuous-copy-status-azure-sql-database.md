---
title: Sys.dm_continuous_copy_status (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: e44ea7c153948db7d7570e25adc5a343c9ecb33a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmcontinuouscopystatus-azure-sql-database"></a>Sys.dm_continuous_copy_status (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada base de datos de usuario (V11) que participa en una relación de copia continua de replicación geográfica. Si se inicia más de una relación de copia continua para una base de datos principal dada, esta tabla contiene una fila por cada base de datos secundaria activa.  
  
Si usas V12 de base de datos de SQL debe usar [sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (porque *sys.dm_continuous_copy_status* sólo se aplica a V11).

  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|Identificador único de la base de datos de réplica.|  
|**partner_server**|**sysname**|Nombre del servidor de SQL Database vinculado.|  
|**partner_database**|**sysname**|Nombre de la base de datos vinculada en la que reside el servidor de SQL Database vinculado.|  
|**last_replication**|**datetimeoffset**|La marca de tiempo de la última transacción replicada aplicada.|  
|**replication_lag_sec**|**int**|Diferencia de tiempo en segundos entre la hora actual y la marca de tiempo de la última transacción confirmada correctamente en la base de datos principal que la base de datos secundaria activa no ha confirmado.|  
|**replication_state**|**tinyint**|El estado de replicación de copia continua para esta base de datos. Éstos son los valores posibles y sus descripciones.<br /><br /> 1: la propagación. El destino de replicación se está inicializando y está en un estado transaccionalmente incoherente. Hasta que la inicialización se completa, no puede conectarse a la base de datos secundaria activa. <br />2: poniendo al día. La base de datos secundaria activa se está poniendo al día con la base de datos principal y está en un estado transaccionalmente coherente.<br />3: volver a la propagación. La base de datos secundaria activa se está reinicializando automáticamente debido a un error de replicación irrecuperable.<br />4: suspendido. Esto no es una relación de copia continua activa. Este estado suele indicar que el ancho de banda disponible para el interlink es insuficiente para el nivel de actividad de transacción en la base de datos principal. Sin embargo, la relación de copia continua sigue intacta.|  
|**replication_state_desc**|**nvarchar(256)**|Descripción del estado de replication_state, uno de los siguientes:<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|Siempre se establece en 0|  
|**is_target_role**|**bit**|0 = Origen de la relación de copia<br /><br /> 1 = Destino de la relación de copia|  
|**is_interlink_connected**|**bit**|1 = Interlink está conectado.<br /><br /> 0 = Interlink está desconectado.|  
  
## <a name="permissions"></a>Permissions  
 Para recuperar datos, debe pertenecer a la **db_owner** rol de base de datos. El usuario dbo, los miembros de la **dbmanager** rol de base de datos y el inicio de sesión de sa pueden consultar esta vista también.  
  
## <a name="remarks"></a>Comentarios  
 El **sys.dm_continuous_copy_status** vista se crea en el **recursos** de base de datos y es visible en todas las bases de datos, incluida la maestra lógica. Sin embargo, al consultar esta vista en la maestra lógica se devuelve un conjunto vacío.  
  
 Si la relación de copia continua se termina en una base de datos, la fila para esa base de datos en el **sys.dm_continuous_copy_status** desaparece de la vista.  
  
 Al igual que el **sys.dm_database_copies** vista, **sys.dm_continuous_copy_status** refleja el estado de la relación de copia continua en el que la base de datos es cualquier primario o activo bases de datos secundarias . A diferencia de **sys.dm_database_copies**, **sys.dm_continuous_copy_status** contiene varias columnas que proporcionan los detalles sobre las operaciones y rendimiento. Estas columnas incluyen **last_replication**, y **replication_lag_sec**...  
  
## <a name="see-also"></a>Vea también  
 [Sys.dm_database_copies &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [Procedimientos almacenados de replicación geográfica activa &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
