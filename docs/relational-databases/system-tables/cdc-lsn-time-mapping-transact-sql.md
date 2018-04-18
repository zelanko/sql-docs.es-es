---
title: CDC.lsn_time_mapping (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d80cb1dd15e66ca6228d2ae1cd31314ddf91c4ff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="cdclsntimemapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada transacción que tiene filas en una tabla de cambios. Esta tabla se utiliza para las asignaciones entre los valores de confirmación de número de secuencia de registro (LSN) y la hora de confirmación de la transacción. También se pueden registrar entradas en las que no se han modificado entradas de tablas. De este modo, la tabla podrá grabar el procesamiento completo del LSN en períodos de baja o nula actividad de cambio.  
  
 Se recomienda que no consulte directamente las tablas del sistema. En su lugar, ejecute el [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) y [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) funciones del sistema.  
    
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|LSN de la transacción confirmada.|  
|**tran_begin_time**|**datetime**|Hora de inicio de la transacción asociada con el LSN.|  
|**tran_end_time**|**datetime**|Hora de finalización de la transacción.|  
|**tran_id**|**varbinary(10)**|Identificador de la transacción.|  
  
## <a name="see-also"></a>Vea también  
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [CDC. &#60;capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
