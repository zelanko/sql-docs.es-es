---
title: Sys.pdw_loader_run_stages (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d209fff76a89f84b67e351864b102ebf8ecbcd5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwloaderrunstages-transact-sql"></a>Sys.pdw_loader_run_stages (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información sobre las operaciones de carga en curso y completadas en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. La información se conserva entre reinicios del sistema.  
  
|||||  
|-|-|-|-|  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|run_id|**int**|Identificador único de un cargador de ejecución.||  
|fase|**nvarchar (30)**|La fase actual de la ejecución.|'CREATE_STAGING', 'DMS_LOAD', 'LOAD_INSERT', 'LOAD_CLEANUP'|  
|request_id|**nvarchar (32)**|Identificador de la solicitud que se ejecuta esta fase.||  
|status|**nvarchar(16)**|Estado de esta fase.||  
|start_time|**datetime**|Hora en que se inició la fase.||  
|end_time|**datetime**|Hora a la que finalizó la fase, si lo hay.|Es NULL si no se ha iniciado o en curso.|  
|total_elapsed_time|**int**|Tiempo total esta fase dedicado (o empleado hasta el momento) de ejecución.|Si total_elapsed_time supera el valor máximo de un entero (24,8 días en milisegundos), provocará el error de materialización debido a desbordamiento.<br /><br /> El valor máximo en milisegundos equivale a días 24,8.|  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
