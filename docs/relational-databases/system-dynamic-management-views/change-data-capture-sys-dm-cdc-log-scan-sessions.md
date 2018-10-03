---
title: Sys.dm_cdc_log_scan_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_log_scan_sessions
- dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], log scan reporting
- sys.dm_cdc_log_scan_sessions dynamic management view
ms.assetid: d337e9d0-78b1-4a07-8820-2027d0b9f87c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d789ec1dd936b7eb40ecae56226a5879754a2260
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698593"
---
# <a name="change-data-capture---sysdmcdclogscansessions"></a>Captura de datos modificados - sys.dm_cdc_log_scan_sessions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada sesión de recorrido de registro de la base de datos actual. La última fila devuelta representa la sesión actual. Puede usar esta vista para devolver información de estado sobre la sesión del recorrido del registro actual, o bien información agregada sobre todas las sesiones desde que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.  
   
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Id. de la sesión.<br /><br /> 0 = los datos devueltos en esta fila son un agregado de todas las sesiones desde que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez.|  
|**start_time**|**datetime**|Hora que la sesión comenzó.<br /><br /> Cuando **session_id** = 0, la hora en que comenzó la recopilación de datos agregados.|  
|**end_time**|**datetime**|Hora a la que finalizó la sesión<br /><br /> NULL = la sesión está activa.<br /><br /> Cuando **session_id** = 0, la hora en que finalizó la última sesión.|  
|**duration**|**bigint**|Duración, en segundos, de la sesión<br /><br /> 0 = la sesión no contiene transacciones de captura de datos de cambio.<br /><br /> Cuando **session_id** = 0, la suma de la duración (en segundos) de todas las sesiones con transacciones de captura de datos de cambio.|  
|**scan_phase**|**nvarchar(200)**|La fase actual de la sesión. Estos son los valores posibles y sus descripciones:<br /><br /> 1: configuración de lectura<br />2: primer examen, generar la tabla hash<br />3: análisis en segundo lugar<br />4: analizar en segundo lugar<br />5: análisis en segundo lugar<br />6: control de versiones de esquema<br />7: último examen<br />8: listo<br /><br /> Cuando **session_id** = 0, este valor siempre es "Aggregate".|  
|**error_count**|**int**|Número máximo de errores detectados<br /><br /> Cuando **session_id** = 0, el número total de errores en todas las sesiones.|  
|**start_lsn**|**nvarchar(23)**|Iniciar LSN para la sesión.<br /><br /> Cuando **session_id** = 0, LSN inicial de la última sesión.|  
|**current_lsn**|**nvarchar(23)**|LSN actual del que se realiza un recorrido.<br /><br /> Cuando **session_id** = 0, el LSN actual es 0.|  
|**end_lsn**|**nvarchar(23)**|LSN final de la sesión.<br /><br /> NULL = la sesión está activa.<br /><br /> Cuando **session_id** = 0, LSN final de la última sesión.|  
|**tran_count**|**bigint**|Número de transacciones de captura de datos de cambio procesados. Este contador se rellena en la fase 2.<br /><br /> Cuando **session_id** = 0, el número de transacciones procesadas en todas las sesiones.|  
|**last_commit_lsn**|**nvarchar(23)**|LSN de la última entrada del registro de confirmación procesada.<br /><br /> Cuando **session_id** = 0, la última entrada de registro de confirmación LSN para cualquier sesión.|  
|**last_commit_time**|**datetime**|Hora de procesamiento de la última entrada del registro de confirmación.<br /><br /> Cuando **session_id** = 0, la hora de entrada de registro de la última confirmación para cualquier sesión.|  
|**log_record_count**|**bigint**|Número de entradas de registro de las que se ha realizado un recorrido.<br /><br /> Cuando **session_id** = 0, número de registros se analizan para todas las sesiones.|  
|**schema_change_count**|**int**|Número de operaciones de lenguaje de definición de datos (DDL) detectadas. Este contador se rellena en la fase 6.<br /><br /> Cuando **session_id** = 0, el número de operaciones DDL procesadas en todas las sesiones.|  
|**command_count**|**bigint**|Número de comandos procesados.<br /><br /> Cuando **session_id** = 0, el número de comandos procesados en todas las sesiones.|  
|**first_begin_cdc_lsn**|**nvarchar(23)**|Primer LSN que contenía las transacciones de captura de los datos de cambio.<br /><br /> Cuando **session_id** = 0, primer LSN que contenía las transacciones de captura de datos de cambio.|  
|**last_commit_cdc_lsn**|**nvarchar(23)**|LSN de la última entrada de registro de confirmación que contenía las transacciones de captura de los datos de cambio.<br /><br /> Cuando **session_id** = 0, la última entrada de registro LSN de confirmación para cualquier sesión que contenía las transacciones de captura de datos de cambio|  
|**last_commit_cdc_time**|**datetime**|Hora de procesamiento de la última entrada de registro de confirmación que contenía las transacciones de captura de los datos de cambio.<br /><br /> Cuando **session_id** = 0, hora del último registro de confirmación que se registre para cualquier sesión que contenía las transacciones de captura de datos de cambio.|  
|**latencia**|**int**|La diferencia, en segundos, entre **end_time** y **last_commit_cdc_time** en la sesión. Este contador se rellena al final de la fase 7.<br /><br /> Cuando **session_id** = 0, el último valor de latencia distinto de cero registrado por una sesión.|  
|**empty_scan_count**|**int**|Número de sesiones consecutivas que no contenían ninguna transacciones de captura de los datos de cambio.|  
|**failed_sessions_count**|**int**|Número de sesiones erróneas.|  
  
## <a name="remarks"></a>Comentarios  
 Se restablecen los valores en esta vista de administración dinámica siempre que se inicia la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE para consultar el **sys.dm_cdc_log_scan_sessions** vista de administración dinámica. Para obtener más información acerca de los permisos en las vistas de administración dinámica, consulte [funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo devuelve información para la sesión más actual.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase  
    error_count, start_lsn, current_lsn, end_lsn, tran_count  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_cdc_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

