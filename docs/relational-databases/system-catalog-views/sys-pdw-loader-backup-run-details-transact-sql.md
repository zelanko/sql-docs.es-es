---
title: Sys.pdw_loader_backup_run_details (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
caps.latest.revision: 9
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 82523cd453a2c4352121655c98a57e0ee4cb173b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180427"
---
# <a name="syspdwloaderbackuprundetails-transact-sql"></a>Sys.pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información detallada, más allá de la información de adicional [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), acerca de la copia de seguridad en curso y completada y las operaciones de restauración en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y sobre en curso y se completa la copia de seguridad y restauración, operaciones de carga en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. La información se conserva entre reinicios del sistema.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador único de una copia de seguridad específica o una restauración que se ejecute.<br /><br /> run_id y pdw_node_id forman la clave para esta vista.||  
|pdw_node_id|**int**|Identificador único de un nodo de dispositivo para el que este registro contiene información.<br /><br /> run_id y pdw_node_id forman la clave para esta vista.|Vea node_id en [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar(16)**|El estado actual de la ejecución.|'CANCELAR', 'COMPLETADA', 'ERROR', 'QUEUED', 'EJECUTANDO'|  
|start_time|**datetime**|Hora en que se inició la operación en este nodo concreto.||  
|end_time|**datetime**|Hora a la que finalizó la operación en este nodo concreto, si lo hay.||  
|total_elapsed_time|**int**|Tiempo total de que la operación se ha estado ejecutando en este nodo concreto.|Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido a desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
|progreso|**int**|Progreso de la operación expresada como un porcentaje.|de 0 a 100|  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
