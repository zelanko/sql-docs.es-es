---
title: sys.dm_pdw_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 331bb44faa2938241de98a6bff08f1e660583c4e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689829"
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las sesiones abierto actualmente o recientemente en el dispositivo. Muestra una fila por cada sesión.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|El identificador de la consulta actual o la última consulta se ejecute (si la sesión finaliza y se estaba ejecutando la consulta en tiempo de finalización). Clave para esta vista.|Es único en todas las sesiones en el sistema.|  
|status|**nvarchar(10)**|Para las sesiones actuales, identifica si la sesión está actualmente activa o inactiva. En las últimas sesiones, la sesión puede mostrar el estado cerrado o eliminado (si se forzó el cierre de la sesión).|'ACTIVE', 'CERRADO', 'IDLE', 'TERMINADA'|  
|request_id|**nvarchar(32)**|El identificador de la consulta actual o la última ejecución de consulta.|Es único en todas las solicitudes en el sistema. Es null si no se ha ejecutado.|  
|security_id|**varbinary(85)**|Id. de seguridad de la entidad de seguridad que ejecuta la sesión.||  
|login_name|**nvarchar(128)**|El nombre de inicio de sesión de la entidad de seguridad que ejecuta la sesión.|Cualquier cadena que se ajuste a las convenciones de nomenclatura de usuario.|  
|login_time|**datetime**|Fecha y hora en que el usuario ha iniciado sesión y se creó esta sesión.|Válido **datetime** antes de la hora actual.|  
|query_count|**int**|El número de consultas/requeststhis sesión ha ejecutado desde la creación de capturas.|Mayor o igual que 0.|  
|is_transactional|**bit**|Captura de una sesión actualmente se encuentra dentro de una transacción o no.|0 para la confirmación automática, 1 para transaccional.|  
|client_id|**nvarchar(255)**|Captura información de cliente para la sesión.|Cualquier cadena válida.|  
|app_name|**nvarchar(255)**|Captura información de nombre de aplicación, opcionalmente, establecer como parte del proceso de conexión.|Cualquier cadena válida.|  
|sql_spid|**int**|El número de Id. del SPID. Use el `session_id` esta sesión. Use la `sql_spid` columna unir a **sys.dm_pdw_nodes_exec_sessions**.<br /><br /> **\*\* Advertencia \* \***  esta columna contiene los SPID cerrados.||  
  
 Para obtener información sobre el número máximo de filas retenidas por esta vista, consulte la sección de metadatos en el [límites de capacidad](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) tema.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
