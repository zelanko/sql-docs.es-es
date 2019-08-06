---
title: sys.dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 72af3975378b2450e51b3880e8814705bb514c1a
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811399"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de todas las solicitudes que se encuentran [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]actualmente o que están activas recientemente en. Muestra una fila por solicitud o consulta.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Clave para esta vista. IDENTIFICADOR numérico único asociado a la solicitud.|Único en todas las solicitudes del sistema.|  
|session_id|**nvarchar(32)**|IDENTIFICADOR numérico único asociado a la sesión en la que se ejecutó esta consulta. Vea [Sys. DM _ &#40;_PDW_EXEC_SESSIONS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Estado actual de la solicitud.|"Running", "Suspended", "completed", "Canceled", "Failed".|  
|submit_time|**datetime**|Hora a la que se envió la solicitud para su ejecución.|**DateTime** válido menor o igual que la hora actual y start_time.|  
|start_time|**datetime**|Hora a la que se inició la ejecución de la solicitud.|NULL para las solicitudes en cola; de lo contrario, la **fecha y** hora válidas es menor o igual que la hora actual.|  
|end_compile_time|**datetime**|Hora a la que el motor completó la compilación de la solicitud.|NULL para las solicitudes que aún no se han compilado; de lo contrario, es un **valor DateTime** válido menor que start_time y menor o igual que la hora actual.|
|end_time|**datetime**|Hora a la que se completó la ejecución de la solicitud, se produjo un error o se canceló.|Null para las solicitudes en cola o activas; de lo contrario, una **fecha y** hora válida menor o igual que la hora actual.|  
|total_elapsed_time|**int**|Tiempo transcurrido en la ejecución desde que se inició la solicitud, en milisegundos.|Entre 0 y la diferencia entre start_time y end_time.</br></br> Si total_elapsed_time supera el valor máximo de un entero, total_elapsed_time seguirá siendo el valor máximo. Esta condición generará la advertencia "se ha superado el valor máximo".</br></br> El valor máximo en milisegundos es el mismo que 24,8 días.|  
|etiqueta|**nvarchar(255)**|Cadena de etiqueta opcional asociada a algunas instrucciones de consulta SELECT.|Cualquier cadena que contenga "a-z", "A-Z", "0-9", "_".|  
|error_id|**nvarchar(36)**|IDENTIFICADOR único del error asociado a la solicitud, si existe.|Vea [Sys. DM _ &#40;_PDW_ERRORS Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); se establece en NULL si no se produjo ningún error.|  
|database_id|**int**|Identificador de la base de datos utilizada por el contexto explícito (por ejemplo, USE DB_X).|Vea ID en [Sys. Databases de &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|comando|**nvarchar(4000)**|Contiene el texto completo de la solicitud enviado por el usuario.|Cualquier consulta o texto de solicitud válido. Las consultas que tienen más de 4000 bytes se truncan.|  
|resource_class|**nvarchar(20)**|La clase de recurso para esta solicitud. Vea **concurrency_slots_used** relacionados en [Sys. DM _ &#40;_pdw_resource_waits Transact-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md).  Para obtener más información sobre las clases de recursos, consulte [clases de recursos & administración de cargas de trabajo](https://docs.microsoft.com/azure/sql-data-warehouse/resource-classes-for-workload-management) |Clases de recursos estáticos</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Clases de recursos dinámicos</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(32)**|La configuración de importancia con la que se envió la solicitud. Las solicitudes con una importancia menor permanecerán en cola en estado suspendido, si se envían solicitudes de mayor importancia.  Las solicitudes con mayor importancia se ejecutarán antes que las solicitudes de menor importancia que se enviaron anteriormente.  Para obtener más información sobre la importancia, vea importancia de la [carga de trabajo](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-importance).  |NULL</br>bajo</br>below_normal</br>normal (valor predeterminado)</br>above_normal</br>alta|
|group_name| |Reservada para uso interno.</br>Se aplica a: Almacenamiento de datos SQL de Azure|
|resource_allocation_percentage| |Reservada para uso interno.</br>Se aplica a: Almacenamiento de datos SQL de Azure|
|result_set_cache|**bit**|Detalla si una consulta finalizada era un acierto de caché de resultados (1) o no (0).|0, 1|
||||
  
 Para obtener información acerca de las filas máximas retenidas en esta vista, consulte la sección de metadatos en el tema [límites de capacidad](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .   
  
## <a name="permissions"></a>Permisos

 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="security"></a>Seguridad

 Sys. DM _ _pdw_exec_requests no filtra los resultados de la consulta según los permisos específicos de la base de datos. Los inicios de sesión con el permiso VIEW SERVER STATE pueden obtener resultados de consulta de resultados para todas las bases de datos  
  
>[!WARNING]  
>Un atacante puede usar sys. DM _ _pdw_exec_requests para recuperar información acerca de objetos de base de datos concretos simplemente con el permiso VIEW SERVER STATE y sin tener un permiso específico de la base de datos.  
  
## <a name="see-also"></a>Vea también

 [Vistas &#40;de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos de TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md) 
