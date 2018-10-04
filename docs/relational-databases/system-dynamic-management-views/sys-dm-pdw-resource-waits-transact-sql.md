---
title: Sys.dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ef5b5b551d06281cef03dbfd68d5bea190126285
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674349"
---
# <a name="sysdmpdwresourcewaits-transact-sql"></a>Sys.dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Información para todos los tipos de recursos en espera de muestra [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posición de la solicitud en la lista de espera.|ordinal basado en 0. Esto no es único en todas las entradas de espera.|  
|session_id|**nvarchar(32)**|Identificador de la sesión en el que se ha producido el estado de espera.|Consulte session_id en [sys.dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|Tipo|**nvarchar(255)**|Tipo de espera que esta entrada representa.|Valores posibles:<br /><br /> Conexión<br /><br /> Simultaneidad de consultas locales<br /><br /> Simultaneidad de las consultas distribuidas<br /><br /> Simultaneidad DMS<br /><br /> Simultaneidad de copia de seguridad|  
|object_type|**nvarchar(255)**|Tipo de objeto que se ve afectado por la espera.|Valores posibles:<br /><br /> **OBJETO**<br /><br /> **DATABASE**<br /><br /> **SYSTEM**<br /><br /> **SCHEMA**<br /><br /> **APLICACIÓN**|  
|object_name|**nvarchar(386)**|Nombre o GUID del objeto especificado que se vio afectado por la espera.|Las tablas y vistas se muestran con nombres de tres partes.<br /><br /> Índices y estadísticas se muestran con nombres de cuatro partes.<br /><br /> Los nombres de las entidades de seguridad y las bases de datos son los nombres de cadena.|  
|request_id|**nvarchar(32)**|Identificador de la solicitud en el que se ha producido el estado de espera.|Identificador QID de la solicitud.<br /><br /> Identificador GUID para las solicitudes de carga.|  
|request_time|**datetime**|Hora a la que se solicitó el bloqueo o recurso.||  
|acquire_time|**datetime**|Hora a la que se adquirió el bloqueo o recurso.||  
|state|**nvarchar(50)**|Estado del estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridad del elemento de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|Número de espacios de simultaneidad (máximo 32) reservado para esta solicitud.|1 – para SmallRC<br /><br /> 3 – para MediumRC<br /><br /> 7 para LargeRC<br /><br /> 22: para XLargeRC|  
|resource_class|**nvarchar (20)**|La clase de recursos para esta solicitud.|SmallRC<br /><br /> MediumRC<br /><br /> LargeRC<br /><br /> XLargeRC|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
