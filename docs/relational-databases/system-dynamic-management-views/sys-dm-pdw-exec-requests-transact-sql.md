---
title: Sys.dm_pdw_exec_requests (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
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
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f6ceea1c7a604b2bfd98a158b383814990644391
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>Sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las solicitudes activas actualmente o que recientemente en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Muestra una fila por cada solicitud o consulta.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Clave para esta vista. Identificador numérico único asociado a la solicitud.|Único en todas las solicitudes en el sistema.|  
|session_id|**nvarchar(32)**|Identificador numérico único asociado a la sesión en el que se ejecute esta consulta. Vea [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Estado actual de la solicitud.|"Running", 'Suspendido', 'Completar', 'Cancelar', 'Error'.|  
|submit_time|**datetime**|Hora a la que se envió la solicitud de ejecución.|Válido **datetime** menor o igual a la hora actual y start_time.|  
|start_time|**datetime**|Hora en que se inició la ejecución de la solicitud.|NULL para las solicitudes en cola; de lo contrario, válido **datetime** menor o igual a la hora actual.|  
|end_compile_time|**datetime**|Hora en que completó el motor de compilación de la solicitud.|NULL para las solicitudes que no se ha compilado todavía; en caso contrario válido **datetime** start_time inferior y menor o igual que la hora actual.|
|end_time|**datetime**|Hora a la que la ejecución de la solicitud completado, error o se canceló.|NULL para las solicitudes en cola o activas; en caso contrario, válido **datetime** menor o igual a la hora actual.|  
|total_elapsed_time|**int**|Tiempo transcurrido en ejecución desde que se inició la solicitud, en milisegundos.|Entre 0 y la diferencia entre start_time y end_time.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|etiqueta|**nvarchar(255)**|Cadena de etiqueta opcional asociada algunas instrucciones de consulta SELECT.|Cualquier cadena que contiene "a-z", "A-z", "0-9', '_'.|  
|error_id|**nvarchar(36)**|Identificador único del error asociado a la solicitud, si lo hay.|Vea [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); establece en NULL si se ha producido ningún error.|  
|database_id|**int**|Identificador de base de datos utilizada explícito de contexto (por ejemplo, utilice DB_X).|Vea el Id. de [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|comando|**nvarchar(4000)**|Contiene el texto completo de la solicitud como enviado por el usuario.|Cualquier texto de consulta o de solicitud válido. Las consultas que tengan más de 4000 bytes se truncan.|  
|resource_class|**nvarchar (20)**|La clase de recursos para esta solicitud. Consulte el artículo relacionado **concurrency_slots_used** en [sys.dm_pdw_resource_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea "Mínimo y máximo valores" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="security"></a>Seguridad  
 Sys.dm_pdw_exec_requests no filtra los resultados de la consulta según los permisos específicos de la base de datos. Inicios de sesión con permiso VIEW SERVER STATE pueden obtener resultados resultados de la consulta para todas las bases de datos  
  
> [!WARNING]  
>  Un atacante puede usar sys.dm_pdw_exec_requests para recuperar información acerca de los objetos de base de datos específica por simplemente tener permiso VIEW SERVER STATE y al no tener un permiso específico de la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
