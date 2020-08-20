---
description: Sys. dm_pdw_nodes (Transact-SQL)
title: Sys. dm_pdw_nodes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 93966909-d758-4d50-950b-f5066d104fa6
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b999f7e10baece4566ebe0dd87b96b92eaabac53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474799"
---
# <a name="sysdm_pdw_nodes-transact-sql"></a>Sys. dm_pdw_nodes (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene información sobre todos los nodos de [!INCLUDE[ssAPS](../../includes/ssaps-md.md)] . Muestra una fila por nodo en el dispositivo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Identificador numérico único asociado al nodo.<br /><br /> Clave para esta vista.|Único en todo el dispositivo, independientemente del tipo.|  
|type|**nvarchar(32)**|Tipo del nodo.|' COMPUTE ', ' CONTROL ', ' MANAGEMENT '|  
|name|**nvarchar(32)**|Nombre lógico del nodo.|Cualquier cadena de longitud adecuada.|  
|address|**nvarchar(32)**|Dirección IP de este nodo.|En el formato de [0-255]. [0-255]. [0-255]. [0-255].|  
|is_passive|**int**|Indica si la máquina virtual que ejecuta el nodo se está ejecutando en el servidor asignado o si se ha conmutado por error al servidor de reserva.|0: la máquina virtual de nodo se está ejecutando en el servidor original.<br /><br /> se está ejecutando una máquina virtual de 1 nodo en el servidor de reserva.|  
|region|**nvarchar(32)**|La región en la que se está ejecutando el nodo.|' PDW ', ' HDINSIGHT '|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
