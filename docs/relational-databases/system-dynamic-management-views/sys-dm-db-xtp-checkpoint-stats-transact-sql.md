---
title: Sys.dm_db_xtp_checkpoint_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_stats
- dm_db_xtp_checkpoint_stats_TSQL
- sys.dm_db_xtp_checkpoint_stats
- sys.dm_db_xtp_checkpoint_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_stats dynamic management view
ms.assetid: 8d0b18ca-db4d-4376-9905-3e4457727c46
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 183970c09d23304553167b20366e0751d5f35207
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993867"
---
# <a name="sysdmdbxtpcheckpointstats-transact-sql"></a>sys.dm_db_xtp_checkpoint_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Devuelve estadísticas sobre las operaciones de punto de comprobación de OLTP en memoria de la base de datos actual. Si la base de datos no tiene objetos de OLTP en memoria, devuelve un conjunto de resultados vacío.  
  
 Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
```  
SELECT * FROM db.sys.dm_db_xtp_checkpoint_stats;  
```  
  
**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] es sustancialmente diferente de las versiones más recientes y se explica inferior en el tema en [SQL Server 2014](#bkmk_2014).**
  
## <a name="includesssql15includessssql15-mdmd-and-later"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores  
 En la tabla siguiente se describe las columnas en `sys.dm_db_xtp_checkpoint_stats`, empezando por **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]**.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|last_lsn_processed|**bigint**|Último LSN visto por el controlador.|  
|end_of_log_lsn|**numeric(38)**|El LSN del final del registro.|  
|bytes_to_end_of_log|**bigint**|Bytes sin procesar por el controlador, correspondientes a los bytes entre registro `last_lsn_processed` y `end_of_log_lsn`.|  
|log_consumption_rate|**bigint**|Tasa de consumo de registro de transacciones por el controlador (en KB/seg).|  
|active_scan_time_in_ms|**bigint**|Tiempo invertido por el controlador en el registro de transacciones.|  
|total_wait_time_in_ms|**bigint**|Tiempo de espera acumulativo para el controlador mientras no realiza el análisis del registro.|  
|waits_for_io|**bigint**|Número de esperas de E/S que se incurre por el subproceso controlador del registro.|  
|io_wait_time_in_ms|**bigint**|Tiempo acumulado empleado en E/S de registro por el subproceso controlador en espera.|  
|waits_for_new_log_count|**bigint**|Número de esperas que se incurre por el subproceso controlador para un nuevo registro a generarse.|  
|new_log_wait_time_in_ms|**bigint**|Tiempo acumulado empleado por el subproceso controlador en espera en un nuevo registro.|  
|idle_attempts_count|**bigint**|Número de veces que el controlador de la transición a un estado de inactividad.|  
|tx_segments_dispatched|**bigint**|Número de segmentos visto por el controlador y enviadas a los serializadores. Segmento es una parte contigua del registro que forman una unidad de la serialización. Actualmente tiene un tamaño a 1MB, pero puede cambiar en el futuro.|  
|segment_bytes_dispatched|**bigint**|Recuento total de bytes de bytes enviado por el controlador para los serializadores, ya que se reinicie la base de datos.|  
|bytes_serialized|**bigint**|Recuento total de bytes serializado, ya que se reinicie la base de datos.|  
|serializer_user_time_in_ms|**bigint**|Tiempo invertido por los serializadores en modo de usuario.|  
|serializer_kernel_time_in_ms|**bigint**|Tiempo invertido por los serializadores en modo kernel.|  
|xtp_log_bytes_consumed|**bigint**|Recuento total de bytes de registro consumidos desde la base de datos que se reinició.|  
|checkpoints_closed|**bigint**|Recuento de puntos de comprobación cerrados desde la base de datos que se reinició.|  
|last_closed_checkpoint_ts|**bigint**|Marca de tiempo del último punto de comprobación cerrado.|  
|hardened_recovery_lsn|**numeric(38)**|Se iniciará la recuperación desde este LSN.|  
|hardened_root_file_guid|**uniqueidentifier**|GUID del archivo raíz que protege como resultado el último punto de comprobación completado.|  
|hardened_root_file_watermark|**bigint**|**Interno sólo**. Cuánto es válido para leer el archivo raíz hasta (este es un tipo pertinente internamente solo – llamado BSN).|  
|hardened_truncation_lsn|**numeric(38)**|LSN del punto de truncamiento.|  
|log_bytes_since_last_close|**bigint**|Bytes desde el último cierre al final del registro actual.|  
|time_since_last_close_in_ms|**bigint**|Hora desde el último cierre del punto de control.|  
|current_checkpoint_id|**bigint**|Segmentos nuevos actualmente se están asignando a este punto de control. El sistema de punto de comprobación es una canalización. El punto de comprobación actual es el que se asignan a segmentos desde el registro. Una vez que ha alcanzado un límite, el punto de control se libera por el controlador y uno creado como actual.|  
|current_checkpoint_segment_count|**bigint**|Recuento de segmentos en el punto de control actual.|  
|recovery_lsn_candidate|**bigint**|**Solo internamente**. Candidato a ser elegido como recoverylsn cuando se cierra current_checkpoint_id.|  
|outstanding_checkpoint_count|**bigint**|Número de puntos de control en la canalización a la espera de cerrarse.|  
|closing_checkpoint_id|**bigint**|Id. del punto de control de cierre.<br /><br /> Los serializadores están trabajando en paralelo, por lo que una vez que han terminado, a continuación, el punto de control es un candidato a cerrado por subproceso cerrado. Pero el subproceso cerrado sólo puede cerrar una vez y debe ser en orden, por lo que el punto de control de cierre es lo que el subproceso cerrado que está trabajando.|  
|recovery_checkpoint_id|**bigint**|Identificador del punto de control que se usará en la recuperación.|  
|recovery_checkpoint_ts|**bigint**|Marca de tiempo del punto de comprobación de recuperación.|  
|bootstrap_recovery_lsn|**numeric(38)**|LSN de recuperación para el arranque.|  
|bootstrap_root_file_guid|**uniqueidentifier**|GUID del archivo raíz para el arranque.|  
|internal_error_code|**bigint**|Error visto por cualquiera del controlador, serializador, cierre y los subprocesos de mezcla.|
|bytes_of_large_data_serialized|**bigint**|La cantidad de datos que se serializan. |  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 En la tabla siguiente se describe las columnas en `sys.dm_db_xtp_checkpoint_stats`, para **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]**.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|log_to_process_in_bytes|**bigint**|El número de bytes de registro entre el número de secuencia de registro (LSN) actual del subproceso y el fin del registro.|  
|total_log_blocks_processed|**bigint**|Número total de bloques de registro procesados desde el inicio del servidor.|  
|total_log_records_processed|**bigint**|Número total de entradas del registro procesadas desde el inicio del servidor.|  
|xtp_log_records_processed|**bigint**|Número total de entradas del registro de OLTP en memoria procesadas desde el inicio del servidor.|  
|total_wait_time_in_ms|**bigint**|Tiempo de espera acumulativo en ms.|  
|waits_for_io|**bigint**|Número de esperas del registro E/S.|  
|io_wait_time_in_ms|**bigint**|Tiempo acumulado empleado en esperar la E/S de registro.|  
|waits_for_new_log|**bigint**|Número de esperas para el nuevo registro que se va a generar.|  
|new_log_wait_time_in_ms|**bigint**|Tiempo acumulado empleado en esperar el nuevo registro.|  
|log_generated_since_last_checkpoint_in_bytes|**bigint**|Cantidad de registro generado desde el último punto de comprobación de OLTP en memoria.|  
|ms_since_last_checkpoint|**bigint**|Cantidad de tiempo en milisegundos desde el último punto de comprobación de OLTP en memoria.|  
|checkpoint_lsn|**numeric (38)**|Número de secuencia de registro (LSN) de recuperación asociada al punto de comprobación OLTP en memoria completado.|  
|current_lsn|**numeric (38)**|El LSN de la entrada de registro que se está procesando actualmente.|  
|end_of_log_lsn|**numeric (38)**|El LSN del final del registro.|  
|task_address|**varbinary (8)**|Dirección de SOS_Task. Combinación con sys.dm_os_tasks para buscar información adicional.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso `VIEW DATABASE STATE` en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de tabla optimizado para memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
