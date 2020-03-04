---
title: Sys. dm_pdw_exec_requests (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 15049436b0d1769361ae1cfc47b52bfb503ba763
ms.sourcegitcommit: 58c25f47cfd701c61022a0adfc012e6afb9ce6e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/03/2020
ms.locfileid: "78256885"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>Sys. dm_pdw_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de todas las solicitudes que se encuentran [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]actualmente o que están activas recientemente en. Muestra una fila por solicitud o consulta.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar (32)**|Clave para esta vista. IDENTIFICADOR numérico único asociado a la solicitud.|Único en todas las solicitudes del sistema.|  
|session_id|**nvarchar (32)**|IDENTIFICADOR numérico único asociado a la sesión en la que se ejecutó esta consulta. Vea [Sys. dm_pdw_exec_sessions &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|status|**nvarchar (32)**|Estado actual de la solicitud.|"Running", "Suspended", "completed", "Canceled", "Failed".|  
|submit_time|**datetime**|Hora a la que se envió la solicitud para su ejecución.|**Fecha** y hora válida, menor o igual que la hora actual y start_time.|  
|start_time|**datetime**|Hora a la que se inició la ejecución de la solicitud.|NULL para las solicitudes en cola; de lo contrario, la **fecha y** hora válidas es menor o igual que la hora actual.|  
|end_compile_time|**datetime**|Hora a la que el motor completó la compilación de la solicitud.|NULL para las solicitudes que aún no se han compilado; de lo contrario, un **valor DateTime** válido menor que start_time y menor o igual que la hora actual.|
|end_time|**datetime**|Hora a la que se completó la ejecución de la solicitud, se produjo un error o se canceló.|Null para las solicitudes en cola o activas; de lo contrario, una **fecha y** hora válida menor o igual que la hora actual.|  
|total_elapsed_time|**int**|Tiempo transcurrido en la ejecución desde que se inició la solicitud, en milisegundos.|Entre 0 y la diferencia entre start_time y end_time.</br></br> Si total_elapsed_time supera el valor máximo de un entero, total_elapsed_time seguirá siendo el valor máximo. Esta condición generará la advertencia "se ha superado el valor máximo".</br></br> El valor máximo en milisegundos es el mismo que 24,8 días.|  
|label|**nvarchar(255)**|Cadena de etiqueta opcional asociada a algunas instrucciones de consulta SELECT.|Cualquier cadena que contenga "a-z", "A-Z", "0-9", "_".|  
|error_id|**nvarchar (36)**|IDENTIFICADOR único del error asociado a la solicitud, si existe.|Vea [Sys. dm_pdw_errors &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md); se establece en NULL si no se produjo ningún error.|  
|database_id|**int**|Identificador de la base de datos utilizada por el contexto explícito (por ejemplo, USE DB_X).|Vea ID en [Sys. databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|command|**nvarchar(4000)**|Contiene el texto completo de la solicitud enviado por el usuario.|Cualquier consulta o texto de solicitud válido. Las consultas que tienen más de 4000 bytes se truncan.|  
|resource_class|**nvarchar (20)**|Grupo de cargas de trabajo que se usa para esta solicitud. |Clases de recursos estáticos</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>Clases de recursos dinámicos</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|La importancia del establecimiento de la solicitud ejecutada a las.  Esta es la importancia relativa de una solicitud en este grupo de cargas de trabajo y entre grupos de cargas de trabajo para los recursos compartidos.  La importancia especificada en el clasificador invalida la configuración de importancia del grupo de cargas de trabajo.</br>Se aplica a: Azure SQL Data Warehouse|NULL</br>bajo</br>below_normal</br>normal (valor predeterminado)</br>above_normal</br>alta|
|group_name|**sysname** |En el caso de las solicitudes que usan recursos, group_name es el nombre del grupo de cargas de trabajo en el que se ejecuta la solicitud.  Si la solicitud no emplea recursos, group_name es NULL.</br>Se aplica a: Azure SQL Data Warehouse|
|classifier_name|**sysname**|Para las solicitudes que usan recursos, el nombre del clasificador utilizado para asignar recursos e importancia.||
|resource_allocation_percentage|**decimal (5, 2)**|La cantidad de recursos asignados a la solicitud.</br>Se aplica a: Azure SQL Data Warehouse|
|result_set_cache|**bit**|Detalla si una consulta completada ha utilizado caché de conjunto de resultados.  </br>Se aplica a: Azure SQL Data Warehouse| 1 = acierto de caché de conjunto de resultados </br> 0 = error de caché de conjunto de resultados </br> Valores negativos = motivos por los que no se ha usado el almacenamiento en caché del conjunto de resultados.  Vea la sección Comentarios para obtener más información.|
||||
  
## <a name="remarks"></a>Observaciones 
 Para obtener información acerca de las filas máximas retenidas en esta vista, consulte la sección de metadatos en el tema [límites de capacidad](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .

 El result_set_cache es una máscara de máscara del uso de la memoria caché del conjunto de resultados de una consulta.  Esta columna puede ser la [| (OR bit a bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) producto de uno o varios de estos valores:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Acierto de caché de conjunto de resultados|  
|-**0x00**|Error de caché de conjunto de resultados|  
|-**0x01**|El almacenamiento en caché del conjunto de resultados está deshabilitado en la base de datos.|  
|-**0x02**|El almacenamiento en caché del conjunto de resultados está deshabilitado en la sesión. | 
|-**0x04**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido a que no hay orígenes de datos para la consulta.|  
|-**0x08**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido a predicados de seguridad de nivel de fila.|  
|-**0x10**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido al uso de la tabla del sistema, la tabla temporal o la tabla externa en la consulta.|  
|-**0x20**|El almacenamiento en caché del conjunto de resultados está deshabilitado porque la consulta contiene constantes de tiempo de ejecución, funciones definidas por el usuario o funciones no deterministas.|  
|-**0x40**|El almacenamiento en caché del conjunto de resultados está deshabilitado debido a que el tamaño del conjunto de resultados Estimado es demasiado grande (> 1 millón filas).|  
|-**0x80**|El almacenamiento en caché del conjunto de resultados está deshabilitado porque el conjunto de resultados contiene filas con un tamaño grande (>64 KB).|  
  
## <a name="permissions"></a>Permisos

 Requiere el permiso VIEW SERVER STATE.  
  
## <a name="security"></a>Seguridad

 Sys. dm_pdw_exec_requests no filtra los resultados de la consulta según los permisos específicos de la base de datos. Los inicios de sesión con el permiso VIEW SERVER STATE pueden obtener resultados de consulta de resultados para todas las bases de datos  
  
>[!WARNING]  
>Un atacante puede usar sys. dm_pdw_exec_requests para recuperar información acerca de objetos de base de datos específicos con solo tener el permiso VIEW SERVER STATE y no tiene permiso específico de la base de datos.  
  
## <a name="see-also"></a>Consulte también

 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
