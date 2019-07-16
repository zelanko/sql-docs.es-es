---
title: syscollector_execution_log_full (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_log_full
- syscollector_execution_log_full_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_execution_log_full view
ms.assetid: 6c8db22d-2e4c-4b7c-ac5a-8762ef1b175b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4bcbbf3d4e0e0b77156b7adceedbdc5aad97afdc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060365"
---
# <a name="syscollectorexecutionlogfull-transact-sql"></a>syscollector_execution_log_full (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información sobre un conjunto o paquete de recopilación cuando el registro de ejecución está lleno.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|log_id|**bigint**|Identifica cada ejecución del conjunto de recopilación. Se usa para combinar esta vista con otros registros detallados. Acepta valores NULL.|  
|parent_log_id|**bigint**|Identifica el conjunto de recopilación o paquete primario. No admite valores NULL. Los identificadores están encadenados en la relación primaria-secundaria, lo que permite determinar qué paquete se inició y con qué conjunto de recopilación. Esta vista agrupa las entradas de registro por su vinculación primaria-secundaria y aplica sangría a los nombres de los paquetes para que la cadena de la llamada esté claramente visible.|  
|name|**nvarchar(4000)**|El nombre del paquete o conjunto de recopilación que representa esta entrada de registro. Acepta valores NULL.|  
|status|**smallint**|Indica el estado actual del paquete o conjunto de recopilación. Acepta valores NULL.<br /><br /> Los valores son:<br /><br /> 0 = en ejecución<br /><br /> 1 = finalizado<br /><br /> 2 = error|  
|runtime_execution_mode|**smallint**|Indica si la actividad del conjunto de recopilación era recopilación de datos o carga de datos. Acepta valores NULL.|  
|start_time|**datetime**|La hora de inicio del paquete o conjunto de recopilación. Acepta valores NULL.|  
|last_iteration_time|**datetime**|Para los paquetes que se ejecutan de manera continua, la última vez que el paquete capturó una instantánea. Acepta valores NULL.|  
|finish_time|**datetime**|La hora de finalización de la ejecución de los conjuntos de recopilación y paquetes completados. Acepta valores NULL.|  
|duration|**int**|El tiempo, en segundos, de ejecución del paquete o conjunto de recopilación. Acepta valores NULL.|  
|failure_message|**nvarchar(2048)**|En caso de error del paquete o conjunto de recopilación, el mensaje de error más reciente para ese componente. Acepta valores NULL. Para obtener información más detallada del error, use la [fn_syscollector_get_execution_details &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md) función.|  
|operador|**nvarchar(128)**|Identifica quién inició el paquete o conjunto de recopilación. Acepta valores NULL.|  
|package_execution_id|**uniqueidentifier**|Proporciona un vínculo a la tabla de registros [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Acepta valores NULL.|  
|collection_set_id|**int**|Proporciona un vínculo a la tabla de configuración de recopilaciones de datos en msdb. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Requiere SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
