---
title: trace_xe_action_map (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 29fba0bc16dc42798ecd37d234dd79e30e9db856
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33256759"
---
# <a name="extended-events-tables---tracexeactionmap"></a>Extended tablas de eventos - trace_xe_action_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada acción de eventos extendidos que se asigna a un identificador de columna de Seguimiento de SQL. Esta tabla se almacena en la base de datos maestra, en el esquema sys.  
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|trace_column_id|**smallint**|El identificador de la columna de Seguimiento de SQL que se asigna.|  
|package_name|**nvarchar(60)**|El nombre del paquete de eventos extendidos donde reside la acción asignada.|  
|xe_action_name|**nvarchar(60)**|El nombre de la acción de eventos extendidos que se asigna a la columna de Seguimiento de SQL.|  
  
## <a name="remarks"></a>Comentarios  
 Puede utilizar la siguiente consulta para identificar las acciones de eventos extendidos que son equivalentes a las columnas de Seguimiento de SQL:  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 Las columnas de Seguimiento de SQL que no se asignan a acciones no se incluyen en la tabla.  
  
## <a name="see-also"></a>Vea también  
 [trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
