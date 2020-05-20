---
title: Sys. dm_cdc_errors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 81908d815818c0274615e9bd2bd3bf40037e2b99
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833851"
---
# <a name="change-data-capture---sysdm_cdc_errors"></a>Captura de datos modificados: sys. dm_cdc_errors
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada error encontrado durante la sesión de recorrido de registro de captura de datos del cambio.  
 
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Id. de la sesión.<br /><br /> 0 = el error no se produjo durante una sesión de recorrido del registro.|  
|**phase_number**|**int**|Número que indica la fase en que se encontraba la sesión en el momento en que se produjo el error. Para obtener una descripción de cada fase, vea [Sys. dm_cdc_log_scan_sessions &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md).|  
|**entry_time**|**datetime**|Fecha y hora de registro del error. Este valor corresponde a la marca de tiempo en el registro de errores de SQL.|  
|**error_number**|**int**|Id. del mensaje de error.|  
|**error_severity**|**int**|Nivel de gravedad del mensaje, entre 1 y 25.|  
|**error_state**|**int**|Número de estado del error.|  
|**error_message**|**nvarchar(1024)**|Texto del mensaje del error.|  
|**start_lsn**|**nvarchar (23)**|Valor LSN inicial de las filas que se estaban procesando en el momento de producirse el error.<br /><br /> 0 = el error no se produjo durante una sesión de recorrido del registro.|  
|**begin_lsn**|**nvarchar (23)**|Valor LSN inicial de la transacción que se estaba procesando en el momento de producirse el error.<br /><br /> 0 = el error no se produjo durante una sesión de recorrido del registro.|  
|**sequence_value**|**nvarchar (23)**|Valor LSN de las filas que se estaban procesando en el momento de producirse el error.<br /><br /> 0 = el error no se produjo durante una sesión de recorrido del registro.|  
  
## <a name="remarks"></a>Observaciones  
 **Sys. dm_cdc_errors** contiene información de error para las sesiones anteriores de 32.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE para consultar la vista de administración dinámica **Sys. dm_cdc_errors** . Para obtener más información acerca de los permisos en las vistas de administración dinámica, vea [funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>Consulte también  
 [Sys. dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [Sys. dm_repl_traninfo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

