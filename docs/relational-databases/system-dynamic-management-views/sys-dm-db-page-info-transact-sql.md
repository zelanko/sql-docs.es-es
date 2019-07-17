---
title: sys.dm_db_page_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_db_page_info
- sys.dm_db_page_info_TSQL
- dm_db_page_info
- dm_db_page_info_TSQL
- dbcc page
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_page_info dynamic management view
author: bluefooted
ms.author: pamela
manager: amitban
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 31b1a282e6d68bf9a31f26536926f9dccd4ff6de
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263820"
---
# <a name="sysdmdbpageinfo-transact-sql"></a>sys.dm_db_page_info (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

Devuelve información sobre una página en una base de datos.  La función devuelve una fila que contiene la información de encabezado en la página, incluido el `object_id`, `index_id`, y `partition_id`.  Esta función reemplaza la necesidad de usar `DBCC PAGE` en la mayoría de los casos.

## <a name="syntax"></a>Sintaxis   
```  
sys.dm_db_page_info ( DatabaseId, FileId, PageId, Mode )  
``` 

## <a name="arguments"></a>Argumentos  
*DatabaseId* | NULL | DEFAULT     
Es el identificador de la base de datos. *DatabaseId* es **smallint**. Una entrada válida es el número de Id. de una base de datos. El valor predeterminado es NULL, pero se envía que un valor NULL para este parámetro producirá un error.
 
*FileId* | NULL | VALOR PREDETERMINADO   
Identificador del archivo. *FileId* es **int**.  La entrada válida es el número de identificación de un archivo en la base de datos especificado por *DatabaseId*. El valor predeterminado es NULL, pero se envía que un valor NULL para este parámetro producirá un error.

*PageId* | NULL | VALOR PREDETERMINADO   
Es el identificador de la página.  *PageId* es **int**.  Una entrada válida es el número de Id. de una página en el archivo especificado por *FileId*. El valor predeterminado es NULL, pero se envía que un valor NULL para este parámetro producirá un error.

*modo* | NULL | VALOR PREDETERMINADO   
Determina el nivel de detalle en la salida de la función. "Limitados" devolverá valores NULL para todas las columnas de descripción, 'DETAILED' rellenar las columnas de descripción.  El valor predeterminado es 'Limitado'.

## <a name="table-returned"></a>Tabla devuelta  

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id |int |Id. de base de datos |
|file_id |int |Id. de archivo |
|page_id |int |Identificador de página |
|page_type |int |Tipo de página |
|page_type_desc |Nvarchar (64) |Descripción del tipo de página |
|page_flag_bits |Nvarchar (64) |Bits de marca de encabezado de página |
|page_flag_bits_desc |nvarchar(256) |Descripción de bits de marca en el encabezado de página |
|page_type_flag_bits |Nvarchar (64) |Bits de marca de tipo en el encabezado de página |
|page_type_flag_bits_desc |Nvarchar (64) |Descripción de bits de la marca de tipo en el encabezado de página |
|object_id |int |Id. de objeto propietario de la página |
|index_id |int |Id. del índice (0 para las páginas de datos del montón) |
|partition_id |bigint |Identificador de la partición |
|alloc_unit_id |bigint |Id. de la unidad de asignación |
|page_level |int |Nivel de la página de índice (hoja = 0) |
|slot_count |smallint |Número total de ranuras (utilizado y no utilizado) <br> Para una página de datos, este número es equivalente al número de filas. |
|ghost_rec_count |smallint |Número de registros marcados como fantasma en la página <br> Un registro fantasma es aquella que se ha marcado para su eliminación pero aún no se puede quitar. |
|torn_bits |int |1 bit por sector para detectar escrituras incompletas. Usa también para almacenar la suma de comprobación <br> Este valor se utiliza para detectar daños en los datos |
|is_iam_pg |bit |Bit para indicar si la página es una página IAM  |
|is_mixed_ext |bit |Bit indicar si asignada en una extensión mixta |
|pfs_file_id |smallint |Id. de archivo de página PFS correspondiente |
|pfs_page_id |int |Identificador de página PFS correspondiente |
|pfs_alloc_percent |int |Porcentaje de asignación según lo indicado en el byte PFS |
|pfs_status |Nvarchar (64) |Byte PFS |
|pfs_status_desc |Nvarchar (64) |Descripción del byte PFS |
|gam_file_id |smallint |Id. de archivo de la página GAM correspondiente |
|gam_page_id |int |Identificador de la página GAM correspondiente |
|gam_status |bit |Bit indicar si asignada en GAM |
|gam_status_desc |Nvarchar (64) |Descripción de la página GAM estado |
|sgam_file_id |smallint |Id. de archivo de la página SGAM correspondiente |
|sgam_page_id |int |Identificador de la página SGAM correspondiente |
|sgam_status |bit |Bit indicar si asignada en SGAM |
|sgam_status_desc |Nvarchar (64) |Descripción de los bits de estado SGAM |
|diff_map_file_id |smallint |Id. de la página correspondiente de mapa de bits diferencial de archivo |
|diff_map_page_id |int |Identificador de la página de mapa de bits diferencial correspondiente |
|diff_status |bit |Bit para indicar si se cambia el estado de diferencias |
|diff_status_desc |Nvarchar (64) |Descripción del bit de estado de diferencias |
|ml_file_id |smallint |Id. de archivo de la página correspondiente de mapa de bits de registro mínimo |
|ml_page_id |int |Identificador de la página de mapa de bits correspondiente registro mínimo |
|ml_status |bit |Bit para indicar si la página se registra al mínimo |
|ml_status_desc |Nvarchar (64) |Descripción del estado de registro mínimo de bits |
|free_bytes |smallint |Número de bytes libres en la página |
|free_data_offset |int |Desplazamiento de espacio libre al final del área de datos |
|reserved_bytes |smallint |Número de bytes libres reservadas por todas las transacciones (si montón) <br> Número de filas fantasmas (si la hoja de índice) |
|reserved_xdes_id |smallint |Espacio que aporta m_xdesID a m_reservedCnt <br> Solo con fines de depuración |
|xdes_id |Nvarchar (64) |Última transacción que aporta m_reserved <br> Solo con fines de depuración |
|prev_page_file_id |smallint |Id. de archivo de página anterior |
|prev_page_page_id |int |Id. de página anterior de página |
|next_page_file_id |smallint |Id. de archivo de página siguiente |
|next_page_page_id |int |Id. de página siguiente de página |
|MIN_LEN |smallint |Longitud de las filas de tamaño fijo |
|lsn |Nvarchar (64) |Número de secuencia de registro / marca de tiempo |
|header_version |int |Versión de encabezado de página |

## <a name="remarks"></a>Comentarios
El `sys.dm_db_page_info` función de administración dinámica devuelve información de la página como `page_id`, `file_id`, `index_id`, `object_id` etc. que se encuentran en un encabezado de página. Esta información es útil para solucionar problemas y depuración de varios problemas de rendimiento (contención de bloqueos y bloqueos temporales) y daños.

`sys.dm_db_page_info` se puede usar en lugar de la `DBCC PAGE` instrucción en muchos casos, pero devuelve solo la información de encabezado de página, no el cuerpo de la página. `DBCC PAGE` seguirán siendo necesarios para los casos de uso que se requieren todo el contenido de la página.

## <a name="using-in-conjunction-with-other-dmvs"></a>Usar junto con otras DMV
Uno de los casos de uso importante de `sys.dm_db_page_info` es combinarla con otras DMV que exponen la información de la página.  Para facilitar este caso de uso, una nueva columna denominada `page_resource` se ha agregado que expone la información de la página en un formato hexadecimal de 8 bytes. Se ha agregado a esta columna `sys.dm_exec_requests` y `sys.sysprocesses` y se agregará a otras DMV en el futuro según sea necesario.

Una nueva función, `sys.fn_PageResCracker`, toma el `page_resource` como entrada y genera una sola fila que contiene `database_id`, `file_id` y `page_id`.  Esta función, a continuación, se puede usar para facilitar las combinaciones entre `sys.dm_exec_requests` o `sys.sysprocesses` y `sys.dm_db_page_info`.

## <a name="permissions"></a>Permisos  
Requiere el `VIEW DATABASE STATE` permiso en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-all-the-properties-of-a-page"></a>A. Mostrar todas las propiedades de una página
La siguiente consulta devuelve una fila con toda la información de página para un determinado `database_id`, `file_id`, `page_id` junto con el modo predeterminado ('limitado')

```sql
SELECT *  
FROM sys.dm_db_page_info (5, 1, 15, DEFAULT)
```

### <a name="b-using-sysdmdbpageinfo-with-other-dmvs"></a>b. Uso de sys.dm_db_page_info con otras DMV 

La siguiente consulta devuelve una fila por cada `wait_resource` expuestos por `sys.dm_exec_requests` cuando la fila contiene un valor no null `page_resource`

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 'LIMITED') AS page_info
```

## <a name="see-also"></a>Vea también  
[Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)     
[sys.fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)


