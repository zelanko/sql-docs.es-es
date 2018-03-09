---
title: MSpeer_conflictdetectionconfigrequest (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- MSpeer_conflictdetectionconfigrequest_TSQL
- MSpeer_conflictdetectionconfigrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_conflictdetectionconfigurerequest
ms.assetid: 83afa0ca-707e-4468-a888-228268ed4e10
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7162681cd957f40a5da0e609124dc3c80624700d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mspeerconflictdetectionconfigrequest-transact-sql"></a>MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza en la replicación punto a punto para realizar el seguimiento de las solicitudes de configuración de toda la topología para una publicación. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifica una solicitud de configuración que produce conflicto. La columna request_id de [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) usa este valor.|  
|publication|**sysname**|Nombre de la publicación desde la que se originó la solicitud de configuración que produce conflicto.|  
|sent_date|**datetime**|Fecha y hora en que se inició la solicitud de configuración que produce conflicto.|  
|timeout|**int**|Período de tiempo que un procedimiento debe esperar para que todos los nodos del mismo nivel devuelvan información de conflicto.|  
|modified_date|**datetime**|Fecha y hora en que se completó una fase.|  
|progress_phase|**nvarchar (32)**|Identifica la fase actual de procesamiento, utilizando uno de los valores siguientes:<br /><br /> Iniciado<br /><br /> Explorando topología<br /><br /> Recopilando estado<br /><br /> Estado recopilado|  
|phase_timed_out|**bit**|Indica si la fase actual ha agotado el tiempo de espera.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
