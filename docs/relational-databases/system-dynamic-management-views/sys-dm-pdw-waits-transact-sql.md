---
description: sys.dm_pdw_waits (Transact-SQL)
title: sys.dm_pdw_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5130e498-1c77-4ae3-a80b-9aae396494e9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 3a3e3e4754b831b28be323c194f9eef70bd64f9b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477196"
---
# <a name="sysdm_pdw_waits-transact-sql"></a>sys.dm_pdw_waits (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene información sobre todos los Estados de espera encontrados durante la ejecución de una solicitud o consulta, incluidos los bloqueos, esperas en las colas de transmisión, etc.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Identificador numérico único asociado al estado de espera.<br /><br /> Clave para esta vista.|Único en todas las esperas en el sistema.|  
|session_id|**nvarchar(32)**|IDENTIFICADOR de la sesión en la que se ha producido el estado de espera.|Vea session_id en [sys.dm_pdw_exec_sessions &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|tipo|**nvarchar(255)**|Tipo de espera que esta entrada representa.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_type|**nvarchar(255)**|Tipo de objeto que se ve afectado por la espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|object_name|**nvarchar (386)**|Nombre o GUID del objeto especificado que se ha visto afectado por la espera.||  
|request_id|**nvarchar(32)**|IDENTIFICADOR de la solicitud en la que se produjo el estado de espera.|Vea request_id en [sys.dm_pdw_exec_requests &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|request_time|**datetime**|Hora a la que se solicitó el estado de espera.||  
|acquire_time|**datetime**|Hora a la que se adquirió el bloqueo o el recurso.||  
|state|**nvarchar(50)**|Estado del estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridad del elemento de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>Consulte también  
 [Azure Synapse Analytics y vistas de administración dinámica de almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_wait_stats &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
  
