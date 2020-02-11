---
title: Sys. dm_pdw_lock_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8ef966f8-d14e-40d3-9626-3508ada9b8fb
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 29a82daa2857177200bd76b738f92d65f6b26668
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67899378"
---
# <a name="sysdm_pdw_lock_waits-transact-sql"></a>Sys. dm_pdw_lock_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre las solicitudes que están en espera de bloqueos.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**BIGINT**|Posición de la solicitud en la lista de espera.|ordinal basado en 0. Esto no es único en todas las entradas de espera.|  
|session_id|**nvarchar (32)**|IDENTIFICADOR de la sesión en la que se ha producido el estado de espera.|Vea session_id en [Sys. dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|type|**nvarchar(255)**|Tipo de espera que esta entrada representa.|Valores posibles:<br /><br /> Compartido<br /><br /> SharedUpdate<br /><br /> ExclusiveUpdate<br /><br /> Exclusivo|  
|object_type|**nvarchar(255)**|Tipo de objeto que se ve afectado por la espera.|Valores posibles:<br /><br /> OBJECT<br /><br /> DATABASE<br /><br /> SYSTEM<br /><br /> SCHEMA<br /><br /> APPLICATION|  
|object_name|**nvarchar (386)**|Nombre o GUID del objeto especificado que se ha visto afectado por la espera.|Las tablas y vistas se muestran con nombres de tres partes.<br /><br /> Los índices y las estadísticas se muestran con nombres de cuatro partes.<br /><br /> Los nombres, entidades de seguridad y bases de datos son nombres de cadena.|  
|request_id|**nvarchar (32)**|IDENTIFICADOR de la solicitud en la que se produjo el estado de espera.|Id. de la solicitud.<br /><br /> Se trata de un GUID para las solicitudes de carga.|  
|request_time|**datetime**|Hora a la que se solicitó el bloqueo o el recurso.||  
|acquire_time|**datetime**|Hora a la que se adquirió el bloqueo o el recurso.||  
|state|**nvarchar(50)**|Estado del estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridad del elemento de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
