---
title: Sys.dm_pdw_dms_cores (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: b3f09b15-0863-4418-9347-a4f5fd2ab7c7
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2c0d681ef3b1d5a7843a955f9e5e0e4a3f69c4e9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38037313"
---
# <a name="sysdmpdwdmscores-transact-sql"></a>sys.dm_pdw_dms_cores (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los servicios DMS, que se ejecutan en los nodos de proceso del dispositivo. Muestra una fila por cada instancia de servicio, que actualmente se encuentra una fila por cada nodo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|dms_core_id|**int**|Identificador numérico único asociado a este centro DMS.<br /><br /> Clave para esta vista.|Se establece en el pdw_node_id del nodo que se está ejecutando este core DMS.|  
|pdw_node_id|**int**|Identificador del nodo en el que se está ejecutando este servicio DMS.|Consulte node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar(32)**|Estado actual del servicio DMS.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
  
 Para obtener información sobre el número máximo de filas retenidas por esta vista, consulte la sección de valores máximos de la vista del sistema en el [valores mínimos y máximos (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
