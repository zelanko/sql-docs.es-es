---
title: Sys.dm_exec_cursors (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cursors_TSQL
- dm_exec_cursors
- dm_exec_cursors_TSQL
- sys.dm_exec_cursors
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_cursors dynamic management function
ms.assetid: f520b63c-36af-40f1-bf71-6901d6331d3d
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b2978fe15394ed17d63c5c98b562a332a629866
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexeccursors-transact-sql"></a>sys.dm_exec_cursors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de los cursores abiertos en diversas bases de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
dm_exec_cursors (session_id | 0 )  
```  
  
## <a name="arguments"></a>Argumentos  
 *session_id* | 0  
 Id. de la sesión. Si *session_id* se especifica, esta función devuelve información acerca de los cursores en la sesión especificada.  
  
 Si se especifica 0, esta función devuelve información acerca de todos los cursores de todas las sesiones.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Id. de la sesión que alberga este cursor.|  
|**cursor_id**|**int**|Id. del objeto de cursor.|  
|**Nombre**|**nvarchar(256)**|Nombre del cursor tal como lo ha definido el usuario.|  
|**propiedades**|**nvarchar(256)**|Especifica las propiedades del cursor. Los valores de las propiedades siguientes se concatenan para formar el valor de esta columna:<br />Interfaz de declaración<br />Tipo de cursor <br />Simultaneidad de cursor<br />Alcance del cursor<br />Nivel de anidamiento de cursor<br /><br /> Por ejemplo, el valor devuelto de esta columna podría ser "TSQL &#124; Dinámica &#124; Optimista &#124; Global (0) ".|  
|**sql_handle**|**varbinary(64)**|Identificador del texto del lote que declaró el cursor.|  
|**statement_start_offset**|**int**|Número de caracteres en el lote que se está ejecutando actualmente o procedimiento almacenado en el que se inicia la instrucción que se está ejecutando actualmente. Puede utilizarse junto con la **sql_handle**, **statement_end_offset**y el [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) función de administración dinámica para recuperar el actualmente ejecutar la instrucción para la solicitud.|  
|**statement_end_offset**|**int**|Número de caracteres en el lote que se está ejecutando actualmente o procedimiento almacenado en el que finaliza la instrucción que se está ejecutando actualmente. Puede utilizarse junto con la **sql_handle**, **statement_start_offset**y el **sys.dm_exec_sql_text** función de administración dinámica para recuperar el actualmente ejecutar la instrucción para la solicitud.|  
|**plan_generation_num**|**bigint**|Número de secuencia que se puede usar para distinguir entre instancias de los planes después de una nueva compilación.|  
|**creation_time**|**datetime**|Marca de tiempo a la que se creó este cursor.|  
|**is_open**|**bit**|Especifica si el cursor está abierto.|  
|**is_async_population**|**bit**|Especifica si el subproceso en segundo plano aún está llenando asincrónicamente un cursor KEYSET o STATIC.|  
|**is_close_on_commit**|**bit**|Especifica si el cursor se declaró mediante CURSOR_CLOSE_ON_COMMIT.<br /><br /> 1 = El cursor se cerrará cuando finalice la transacción.|  
|**FETCH_STATUS**|**int**|Devuelve el estado de la última recopilación del cursor. Esta es la última que devuelve@FETCH_STATUS valor.|  
|**fetch_buffer_size**|**int**|Devuelve información acerca del tamaño del búfer de lectura.<br /><br /> 1 = Cursores Transact-SQL. Se puede establecer en un valor mayor para los cursores API.|  
|**fetch_buffer_start**|**int**|Para cursores FAST_FORWARD y DYNAMIC, devuelve 0 si el cursor no está abierto o si se ha colocado antes de la primera fila. De lo contrario, devuelve -1.<br /><br /> Para cursores STATIC y KEYSET, devuelve 0 si el cursor no está abierto y -1 si se ha colocado después de la última fila.<br /><br /> De lo contrario, devuelve el número de fila en la que se ha colocado.|  
|**ansi_position**|**int**|Posición del cursor en el búfer de lectura.|  
|**valor de worker_time**|**bigint**|Tiempo empleado, en microsegundos, por los trabajadores que ejecutan este cursor.|  
|**lecturas**|**bigint**|Número de lecturas realizadas por el cursor.|  
|**escribe**|**bigint**|Número de escrituras realizadas por el cursor.|  
|**dormant_duration**|**bigint**|Milisegundos desde que se inició la última consulta (abierta o capturada) en este cursor.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se proporciona información acerca de la interfaz de la declaración del cursor y se incluyen los valores posibles para la columna de propiedades.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|API|El cursor se declaró mediante una de las API de acceso a datos (ODBC, OLEDB).|  
|TSQL|El cursor se declaró mediante la sintaxis Transact-SQL DECLARE CURSOR.|  
  
 En la tabla siguiente se proporciona información acerca del tipo de cursor y se incluyen los valores posibles para la columna de propiedades.  
  
|Tipo|Description|  
|----------|-----------------|  
|Keyset|El cursor se ha declarado como de conjunto de claves.|  
|Dynamic|El cursor se ha declarado como dinámico.|  
|Snapshot|El cursor se ha declarado como instantánea o estático.|  
|Fast_Forward|El cursor se ha declarado como de avance rápido.|  
  
 En la tabla siguiente se proporciona información acerca de la simultaneidad de cursor y se incluyen los valores posibles para la columna de propiedades.  
  
|Simultaneidad|Description|  
|-----------------|-----------------|  
|Solo lectura|El cursor se ha declarado como de solo lectura.|  
|Scroll Locks|El cursor utiliza bloqueos de desplazamiento.|  
|Optimistic|El cursor utiliza control de simultaneidad optimista.|  
  
 En la tabla siguiente se proporciona información acerca del alcance del cursor y se incluyen los valores posibles para la columna de propiedades.  
  
|Ámbito|Description|  
|-----------|-----------------|  
|Local|Especifica que el alcance del cursor es local para el proceso por lotes, procedimiento almacenado o desencadenador en que se creó el cursor.|  
|Global|Especifica que el alcance del cursor es global para la conexión.|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-detecting-old-cursors"></a>A. Detectar cursores antiguos  
 En este ejemplo se devuelve información acerca de los cursores que llevan abiertos en el servidor más tiempo del especificado de 36 horas.  
  
```  
SELECT creation_time, cursor_id, name, c.session_id, login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s ON c.session_id = s.session_id   
WHERE DATEDIFF(hh, c.creation_time, GETDATE()) > 36;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica &#40; relacionada con la ejecución Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
  

