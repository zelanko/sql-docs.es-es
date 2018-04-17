---
title: Sys.dm_pdw_dms_cores (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b3f09b15-0863-4418-9347-a4f5fd2ab7c7
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 7c39f5049b76c953c08ca75efcc174ac05dbf2b6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmpdwdmscores-transact-sql"></a>sys.dm_pdw_dms_cores (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los servicios DMS ejecutando de los nodos de la aplicación. Muestra una fila por cada instancia de servicio, que actualmente tiene una fila por cada nodo.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|**int**|Identificador numérico único asociado a este núcleo DMS.<br /><br /> Clave para esta vista.|Se establece en el pdw_node_id del nodo que se está ejecutando este núcleo DMS.|  
|pdw_node_id|**int**|Identificador del nodo en el que se ejecuta este servicio DMS.|Vea node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar(32)**|Estado actual del servicio DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea la sección valores máximos de vista de sistema en el [valores mínimo y máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
