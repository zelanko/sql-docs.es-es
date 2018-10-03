---
title: Sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c2a1978aeea7ec69ea45bc088bbdff432de3c9f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621873"
---
# <a name="sysdmpdwexecrequests-transact-sql"></a>Sys.dm_pdw_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las solicitudes activas actualmente o recientemente en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Muestra una fila por cada solicitud o consulta.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Clave para esta vista. Identificador numérico único asociado a la solicitud.|Es único en todas las solicitudes en el sistema.|  
|session_id|**nvarchar(32)**|Identificador numérico único asociado con la sesión en el que se ejecutó esta consulta. Consulte [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Estado actual de la solicitud.|'Ejecutar', 'Suspendido', 'Completado', 'Cancelar', 'Error'.|  
|submit_time|**datetime**|Hora a la que se envió la solicitud para su ejecución.|Válido **datetime** menor o igual a la hora actual y start_time.|  
|start_time|**datetime**|Hora a la que se inició la ejecución de la solicitud.|NULL para las solicitudes en cola; de lo contrario, válido **datetime** menor o igual que la hora actual.|  
|end_compile_time|**datetime**|Hora en que completó el motor de compilación de la solicitud.|NULL para las solicitudes que no se han compilado aún; en caso contrario válido **datetime** start_time inferior y menor o igual a la hora actual.|
|end_time|**datetime**|Hora a la que la ejecución de la solicitud completado, error o se canceló.|NULL para las solicitudes en cola o activas; en caso contrario, válido **datetime** menor o igual que la hora actual.|  
|total_elapsed_time|**int**|Tiempo transcurrido en ejecución desde que se inició la solicitud, en milisegundos.|Entre 0 y la diferencia entre start_time y end_time.<br /><br /> Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo."<br /><br /> El valor máximo en milisegundos equivale a 24,8 días.|  
|etiqueta|**nvarchar(255)**|Cadena de etiqueta opcional asociada con algunas instrucciones de consulta SELECT.|Cualquier cadena que contiene "a-z", "A-z", "0-9', '_'.|  
|error_id|**nvarchar(36)**|Identificador único del error asociado a la solicitud, si existe.|Consulte [sys.dm_pdw_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); se establece en NULL si se ha producido ningún error.|  
|database_id|**int**|Identificador de base de datos usada el contexto explícito (por ejemplo, USE DB_X).|Vea el Id. de [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|comando|**nvarchar(4000)**|Contiene el texto completo de la solicitud como enviado por el usuario.|Cualquier texto de consulta o de solicitud válido. Las consultas que duran más de 4000 bytes se truncan.|  
|resource_class|**nvarchar (20)**|La clase de recursos para esta solicitud. Consulte el artículo relacionado **concurrency_slots_used** en [sys.dm_pdw_resource_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
 Para obtener información sobre el número máximo de filas retenidas por esta vista, vea "Como mínimo y máximo Values" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="security"></a>Seguridad  
 Sys.dm_pdw_exec_requests no filtra los resultados de la consulta según los permisos específicos de la base de datos. Inicios de sesión con el permiso VIEW SERVER STATE pueden obtener los resultados de los resultados de consulta para todas las bases de datos  
  
> [!WARNING]  
>  Un atacante puede usar sys.dm_pdw_exec_requests para recuperar información acerca de los objetos de base de datos específica por el solo hecho de tener permiso VIEW SERVER STATE y al no tener un permiso específico de la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
