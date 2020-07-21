---
title: Sys. pdw_loader_backup_run_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 04fc004f-ee15-4d7a-be08-78357aa99b55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0a0837b713f5c17f9bfb0357b9b1d999a1338e71
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197182"
---
# <a name="syspdw_loader_backup_run_details-transact-sql"></a>Sys. pdw_loader_backup_run_details (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene información detallada adicional, más allá de la información de [Sys. pdw_loader_backup_runs &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md), acerca de las operaciones de copia de seguridad y restauración en curso y completadas en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y sobre las operaciones de copia de seguridad, restauración y carga en curso y completadas en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] . La información se conserva entre reinicios del sistema.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|Identificador único para una ejecución de restauración o copia de seguridad específica.<br /><br /> run_id y pdw_node_id forman la clave de esta vista.||  
|pdw_node_id|**int**|Identificador único de un nodo de dispositivo para el que este registro contiene detalles.<br /><br /> run_id y pdw_node_id forman la clave de esta vista.|Vea node_id en [Sys. dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|status|**nvarchar (16)**|Estado actual de la ejecución.|' CANCELADO ', ' COMPLETED ', ' FAILED ', ' QUEUED ', ' RUNNING '|  
|start_time|**datetime**|Hora a la que se inició la operación en este nodo concreto.||  
|end_time|**datetime**|Hora a la que finalizó la operación en este nodo determinado, si existe.||  
|total_elapsed_time|**int**|Tiempo total que se ha estado ejecutando la operación en este nodo concreto.|Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), se producirá un error de materialización debido al desbordamiento.<br /><br /> El valor máximo en milisegundos es equivalente a 24,8 días.|  
|progreso|**int**|Progreso de la operación expresado en forma de porcentaje.|De 0 a 100|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
