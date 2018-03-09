---
title: MSrepl_errors (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66c276d57f2df480d1d3977304911c2826068cce
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msreplerrors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSrepl_errors** tabla contiene filas con información ampliada de errores de agente de distribución y agente de mezcla. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|El identificador del error.|  
|**time**|**datetime**|Hora del error.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|Id. de tipo de origen del error|  
|**source_name**|**nvarchar (100)**|Nombre del origen del error.|  
|**error_code**|**sysname**|Código de error.|  
|**error_text**|**ntext**|Mensaje de error.|  
|**xact_seqno**|**varbinary (16)**|Número de secuencia de registro de la transacción inicial del lote de ejecución erróneo. Solo lo utilizan los Agentes de distribución; se trata del número de secuencia del registro de transacciones de la primera transacción en el proceso por lotes de ejecución errónea.|  
|**command_id**|**int**|Id. del comando del proceso por lotes de ejecución fallida. Solo lo utilizan los Agentes de distribución, y se trata del Id. del comando del primer comando del proceso por lotes de ejecución fallida.|  
|**session_id**|**int**|Id. de la sesión del agente en la que ocurrió el error.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
