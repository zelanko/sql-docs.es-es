---
title: Sys.dm_pdw_exec_sessions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6694f2bbd8c8d7a8138a53cb9d8f158c726df6ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwexecsessions-transact-sql"></a>Sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las sesiones abiertas actualmente o que recientemente en el dispositivo. Muestra una fila por cada sesión.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|El identificador de la consulta actual o la última consulta ejecutar (si se finaliza la sesión y se ejecuta la consulta en tiempo de finalización). Clave para esta vista.|Es único en todas las sesiones en el sistema.|  
|status|**nvarchar (10)**|Para las sesiones actuales, indica si la sesión está actualmente activa o inactiva. En las últimas sesiones, la sesión puede mostrar el estado cerrado o eliminado (si se forzó el cierre de la sesión).|'ACTIVE', 'CERRADO', 'INACTIVO', 'TERMINADA'|  
|request_id|**nvarchar(32)**|El identificador de la consulta actual o último ejecutar.|Único en todas las solicitudes en el sistema. Es null si no se ha ejecutado.|  
|security_id|**varbinary(85)**|Id. de seguridad de la entidad de seguridad que se ejecuta la sesión.||  
|login_name|**nvarchar(128)**|El nombre de inicio de sesión de la entidad de seguridad que se ejecuta la sesión.|Cualquier cadena que se ajuste a las convenciones de nomenclatura de usuario.|  
|login_time|**datetime**|Fecha y hora en que el usuario inició sesión y se creó esta sesión.|Válido **datetime** anterior a la hora actual.|  
|query_count|**int**|Captura el número de consultas/requeststhis sesión se ha ejecutado desde que se creó.|Mayor o igual que 0.|  
|is_transactional|**bit**|Captura de una sesión actualmente se encuentra dentro de una transacción o no.|0 para la confirmación automática, 1 para transaccional.|  
|client_id|**nvarchar(255)**|Captura información de cliente para la sesión.|Cualquier cadena válida.|  
|app_name|**nvarchar(255)**|Captura información de nombre de aplicación, opcionalmente, establecer como parte del proceso de conexión.|Cualquier cadena válida.|  
|sql_spid|**int**|El número de identificación de lo SPID. Use la `session_id` esta sesión. Use la `sql_spid` columna que se va a unir a **sys.dm_pdw_nodes_exec_sessions**.<br /><br /> **\*\* Advertencia \* \***  esta columna contiene SPID cerrados.||  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea la sección valores máximos de vista de sistema en el [valores mínimo y máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
