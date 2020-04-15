---
title: sys.dm_pdw_exec_requests (Transact-SQL) Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
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
ms.openlocfilehash: 851c138e00300a303b1618041a16e2c38516968e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301275"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys.dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las solicitudes [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]activas actualmente o recientemente en . Enumera una fila por solicitud/consulta.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Clave para esta vista. ID numérico único asociado a la solicitud.|Es único en todas las solicitudes del sistema.|  
|session_id|**nvarchar(32)**|Identificador numérico único asociado a la sesión en la que se ejecutó esta consulta. Consulte [sys.dm_pdw_exec_sessions &#40;Transact-SQLTransact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar(32)**|Estado actual de la solicitud.|'Running', 'Suspended', 'Completed', 'Canceled', 'Failed'.|  
|submit_time|**datetime**|Hora en que se envió la solicitud para su ejecución.|Fecha **y hora** válida menor o igual que la hora actual y start_time.|  
|start_time|**datetime**|Hora en la que se inició la ejecución de la solicitud.|NULL para solicitudes en cola; de lo contrario, **fecha y hora** válida menor o igual a la hora actual.|  
|end_compile_time|**datetime**|Hora en la que el motor completó la compilación de la solicitud.|NULL para las solicitudes que aún no se han compilado; de lo contrario una **fecha y hora** válida inferior a start_time y menor o igual que la hora actual.|
|end_time|**datetime**|Hora en la que la ejecución de la solicitud se completó, produjo un error o se canceló.|Nulo para solicitudes en cola o activas; de lo contrario, una **fecha y hora** válida menor o igual a la hora actual.|  
|total_elapsed_time|**int**|Tiempo transcurrido en la ejecución desde que se inició la solicitud, en milisegundos.|Entre 0 y la diferencia entre start_time y end_time.</br></br> Si total_elapsed_time supera el valor máximo de un entero, total_elapsed_time seguirá siendo el valor máximo. Esta condición generará la advertencia "Se ha superado el valor máximo."</br></br> El valor máximo en milisegundos es el mismo que 24,8 días.|  
|etiqueta|**nvarchar(255)**|Cadena de etiqueta opcional asociada a algunas instrucciones de consulta SELECT.|Cualquier cadena que contenga 'a-z','A-Z','0-9','_'.|  
|error_id|**nvarchar(36)**|ID único del error asociado a la solicitud, si existe.|Consulte [sys.dm_pdw_errors &#40;&#41;de Transact-SQLTransact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); establecido en NULL si no se produjo ningún error.|  
|database_id|**int**|Identificador de la base de datos utilizada por el contexto explícito (por ejemplo, USE DB_X).|Consulte ID en [sys.databases &#40;Transact-SQLTransact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Contiene el texto completo de la solicitud tal como ha sido enviado por el usuario.|Cualquier consulta o texto de solicitud válido. Las consultas que tienen más de 4000 bytes se truncan.|  
|resource_class|**nvarchar(20)**|El grupo de cargas de trabajo utilizado para esta solicitud. |Clases de recursos estáticos</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Clases de recursos dinámicos</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|Importancia establecer la solicitud ejecutada en.  Esta es la importancia relativa de una solicitud en este grupo de cargas de trabajo y entre grupos de cargas de trabajo para recursos compartidos.  La importancia especificada en el clasificador reemplaza la configuración de importancia del grupo de cargas de trabajo.</br>Se aplica a: Azure SQL Data Warehouse|NULL</br>low</br>below_normal</br>normal (predeterminado)</br>above_normal</br>high|
|group_name|**sysname** |Para las solicitudes que utilizan recursos, group_name es el nombre del grupo de cargas de trabajo en el que se ejecuta la solicitud.  Si la solicitud no utiliza recursos, group_name es null.</br>Se aplica a: Azure SQL Data Warehouse|
|classifier_name|**sysname**|Para las solicitudes que utilizan recursos, el nombre del clasificador utilizado para asignar recursos e importancia.||
|resource_allocation_percentage|**decimal(5,2)**|La cantidad porcentual de recursos asignados a la solicitud.</br>Se aplica a: Azure SQL Data Warehouse|
|result_cache_hit|**Hexadecimal**|Detalla si una consulta completada utiliza la caché del conjunto de resultados.  </br>Se aplica a: Azure SQL Data Warehouse| 1 - Golpe de caché del conjunto de resultados </br> 0 • Error de caché del conjunto de resultados </br> Valores negativos: motivos por los que no se ha utilizado el almacenamiento en caché del conjunto de resultados.  Consulte la sección de comentarios para obtener más información.|
||||
  
## <a name="remarks"></a>Observaciones 
 Para obtener información sobre las filas máximas retenidas por esta vista, consulte la sección Metadatos en el tema Límites de [capacidad.](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)

 El result_cache_hit es una máscara de bits del uso de caché de conjuntos de resultados por parte de una consulta.  Esta columna puede ser la [de la (Or bita)](../../t-sql/language-elements/bitwise-or-transact-sql.md) producto de uno o más de estos valores:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Golpe de caché del conjunto de resultados|  
|-**0x00**|Error de caché del conjunto de resultados|  
|-**0x01**|El almacenamiento en caché del conjunto de resultados está deshabilitado en la base de datos.|  
|-**0x02**|El almacenamiento en caché del conjunto de resultados está deshabilitado en la sesión. | 
|-**0x04**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido a que no hay orígenes de datos para la consulta.|  
|-**0x08**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido a los predicados de seguridad de nivel de fila.|  
|-**0x10**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido al uso de la tabla del sistema, la tabla temporal o la tabla externa en la consulta.|  
|-**0x20**|El almacenamiento en caché del conjunto de resultados está deshabilitado porque la consulta contiene constantes en tiempo de ejecución, funciones definidas por el usuario o funciones no deterministas.|  
|-**0x40**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido a que el tamaño estimado del conjunto de resultados es demasiado grande (> 1 millón de filas).|  
|-**0x80**|El almacenamiento en caché del conjunto de resultados está deshabilitado porque el conjunto de resultados contiene filas de gran tamaño (>64 kb).|  
  
## <a name="permissions"></a>Permisos

 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="security"></a>Seguridad

 sys.dm_pdw_exec_requests no filtra los resultados de la consulta según los permisos específicos de la base de datos. Los inicios de sesión con el permiso VIEW SERVER STATE pueden obtener resultados de consulta para todas las bases de datos  
  
>[!WARNING]  
>Un atacante puede usar sys.dm_pdw_exec_requests para recuperar información sobre objetos de base de datos específicos simplemente teniendo el permiso VIEW SERVER STATE y no tener permiso específico de la base de datos.  
  
## <a name="see-also"></a>Consulte también

 [SQL Data Warehouse y las vistas de administración dinámica de almacenamiento de datos paralelos &#40;Transact-SQLTransact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
