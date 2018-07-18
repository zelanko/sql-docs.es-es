---
title: Sys.dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3f307d70f7c161743d81c33916046e88cadad9e9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37980573"
---
# <a name="sysdmpdwnodes-transact-sql"></a>Sys.dm_pdw_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los nodos en [!INCLUDE[ssAPS](../../includes/ssaps-md.md)]. Muestra una fila por cada nodo en el dispositivo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.<br /><br /> Clave para esta vista.|Es único en todo el dispositivo, independientemente del tipo.|  
|Tipo|**nvarchar(32)**|Tipo del nodo.|'ADMINISTRACIÓN DE PROCESO', 'CONTROL',' '|  
|NAME|**nvarchar(32)**|Nombre lógico del nodo.|Cualquier cadena de longitud adecuada.|  
|address|**nvarchar(32)**|Dirección IP de este nodo.|En el formato de [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|Indica si la máquina virtual ejecuta el nodo se está ejecutando en el servidor asignado o se ha conmutado por error para el servidor de reserva.|0: máquina virtual del nodo se está ejecutando en el servidor original.<br /><br /> 1: máquina virtual del nodo se está ejecutando en el servidor de reserva.|  
|región|**nvarchar(32)**|La región donde se está ejecutando el nodo.|'PDW', 'HDINSIGHT'|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
