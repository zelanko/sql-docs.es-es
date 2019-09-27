---
title: sys.dm_exec_compute_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODES_TSQL
- DM_EXEC_COMPUTE_NODES
- SYS.DM_EXEC_COMPUTE_NODES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_nodes management view
- PolyBase, views
- PolyBase management views
- dm_exec_compute_nodes management view
ms.assetid: 0de4b7a4-401f-4e2d-9ab0-c54587e05154
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44664805dc9b728ecbd48acbf38c4565601c631a
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326145"
---
# <a name="sysdm_exec_compute_nodes-transact-sql"></a>sys.dm_exec_compute_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de los nodos usados con la administración de datos de polybase. Muestra una fila por nodo.  
  
 Use esta DMV para ver la lista de todos los nodos del clúster de escalabilidad horizontal con su rol, el nombre y la dirección IP.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|Identificador numérico único asociado al nodo. Clave para esta vista.|Único en todo el clúster de escalado horizontal, independientemente del tipo.|  
|type|**nvarchar(32)**|Tipo del nodo.|' COMPUTE ', ' HEAD '|  
|name|**nvarchar(32)**|Nombre lógico del nodo.|Cualquier cadena de longitud adecuada.|  
|address|**nvarchar(32)**|Dirección IP de este nodo.|Intervalo de direcciones IP|  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de polybase con vistas de administración dinámica](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas &#40;de administración dinámica relacionadas con bases de datos TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
