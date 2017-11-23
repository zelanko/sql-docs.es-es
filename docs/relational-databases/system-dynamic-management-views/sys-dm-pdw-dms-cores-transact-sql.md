---
title: Sys.dm_pdw_dms_cores (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: b3f09b15-0863-4418-9347-a4f5fd2ab7c7
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1194f0f370d947e14a93f1ebc33f05fb8517f1e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwdmscores-transact-sql"></a>Sys.dm_pdw_dms_cores (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los servicios DMS ejecutando de los nodos de la aplicación. Muestra una fila por cada instancia de servicio, que actualmente tiene una fila por cada nodo.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|**int**|Identificador numérico único asociado a este núcleo DMS.<br /><br /> Clave para esta vista.|Se establece en el pdw_node_id del nodo que se está ejecutando este núcleo DMS.|  
|pdw_node_id|**int**|Identificador del nodo en el que se ejecuta este servicio DMS.|Vea node_id en [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar (32)**|Estado actual del servicio DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea la sección valores máximos de vista de sistema en el [valores mínimo y máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
