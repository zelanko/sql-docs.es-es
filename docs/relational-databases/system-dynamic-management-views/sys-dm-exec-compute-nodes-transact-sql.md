---
title: Sys.dm_exec_compute_nodes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DM_EXEC_COMPUTE_NODES_TSQL
- DM_EXEC_COMPUTE_NODES
- SYS.DM_EXEC_COMPUTE_NODES_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.dm_exec_compute_nodes management view
- PolyBase, views
- PolyBase management views
- dm_exec_compute_nodes management view
ms.assetid: 0de4b7a4-401f-4e2d-9ab0-c54587e05154
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4affdf5cdcab66ffacab6bb40596855938ad1b98
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexeccomputenodes-transact-sql"></a>Sys.dm_exec_compute_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información acerca de los nodos que se utiliza con la administración de datos de PolyBase. Muestra una fila por cada nodo.  
  
 Utilice esta DMV para ver la lista de todos los nodos del clúster de escalabilidad horizontal con su rol, el nombre y la dirección IP.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|compute_node_id|**int**|Identificador numérico único asociado al nodo. Clave para esta vista.|Es único en el clúster de escalabilidad horizontal independientemente del tipo.|  
|Tipo|**nvarchar (32)**|Tipo del nodo.|'COMPUTE', 'PRINCIPAL'|  
|name|**nvarchar (32)**|Nombre lógico del nodo.|Cualquier cadena de longitud apropiada.|  
|address|**nvarchar (32)**|Dirección de P de este nodo.|Intervalo de direcciones IP|  
  
## <a name="see-also"></a>Vea también  
 [PolyBase, solución de problemas con las vistas de administración dinámica](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Base de datos relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
