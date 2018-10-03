---
title: Sys.dm_pdw_lock_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2e60f30972eb98e0b02ce38a142d018c37a56768
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630553"
---
# <a name="sysdmpdwlockwaits-transact-sql"></a>Sys.dm_pdw_lock_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de las solicitudes que están esperando bloqueos.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posición de la solicitud en la lista de espera.|ordinal basado en 0. Esto no es único en todas las entradas de espera.|  
|session_id|**nvarchar(32)**|Identificador de la sesión en el que se ha producido el estado de espera.|Consulte session_id en [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Tipo|**nvarchar(255)**|Tipo de espera que esta entrada representa.|Valores posibles:<br /><br /> Compartidos<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> Exclusivo|  
|object_type|**nvarchar(255)**|Tipo de objeto que se ve afectado por la espera.|Valores posibles:<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar(386)**|Nombre o GUID del objeto especificado que se vio afectado por la espera.|Las tablas y vistas se muestran con nombres de tres partes.<br /><br /> Índices y estadísticas se muestran con nombres de cuatro partes.<br /><br /> Los nombres de las entidades de seguridad y las bases de datos son los nombres de cadena.|  
|request_id|**nvarchar(32)**|Identificador de la solicitud en el que se ha producido el estado de espera.|Identificador de la solicitud.<br /><br /> Se trata de un GUID para las solicitudes de carga.|  
|request_time|**datetime**|Hora a la que se solicitó el bloqueo o recurso.||  
|acquire_time|**datetime**|Hora a la que se adquirió el bloqueo o recurso.||  
|state|**nvarchar(50)**|Estado del estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridad del elemento de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
