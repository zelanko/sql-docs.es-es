---
title: Sys. dm_exec_dms_services (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DMS_SERVICES_TSQL
- SYS.DM_EXEC_DMS_SERVICES_TSQL
- DM_EXEC_DMS_SERVICES
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- PolyBase
- dm_exec_dms_services management view
- sys.dm_exec_dms_services management view
ms.assetid: 6ac47eef-4293-46b8-8555-07a614837504
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11e353af23c2331cd8f2bef5b439c967512e7323
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532934"
---
# <a name="sysdm_exec_dms_services-transact-sql"></a>sys.dm_exec_dms_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los servicios DMS que se ejecutan en los nodos de proceso de polybase. Muestra una fila por cada instancia de servicio.  
  
|Column Name|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|`int`|Identificador numérico único asociado a DMS Core. Clave para esta vista.|IDENTIFICADOR único.|  
|compute_node_id|`int`|IDENTIFICADOR del nodo en el que se está ejecutando este servicio DMS|Vea *compute_node_id* en [Sys. DM_EXEC_COMPUTE_NODES &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md).|  
|status|`nvarchar(32)`|Estado actual del servicio DMS||
|compute_pool_id|`int`|Identificador único para el grupo.|

## <a name="see-also"></a>Vea también  
 [Solución de problemas de polybase con vistas de administración dinámica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas &#40;de administración dinámica relacionadas con bases de datos TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
