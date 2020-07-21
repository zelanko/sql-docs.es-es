---
title: Sys. conversation_priorities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_priorities_TSQL
- conversation_priorities
- sys.conversation_priorities_TSQL
- sys.conversation_priorities
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], priorities
- Service Broker, conversations
- sys.conversation_priorities catalog view
ms.assetid: 7cbb9171-3310-4aae-8458-755c882d6462
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0c0d365978fa8c8c336040db50655e96234ecb22
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887629"
---
# <a name="sysconversation_priorities-transact-sql"></a>sys.conversation_priorities (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila para cada prioridad de conversación creada en la base de datos actual, como se muestra en la tabla siguiente: 
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|Priority_id|**int**|Número que identifica de forma única la prioridad de conversación. No acepta valores NULL.|  
|name|**sysname**|Nombre de la prioridad de conversación. No acepta valores NULL.|  
|service_contract_id|**int**|El identificador del contrato que se especifica para la prioridad de conversación. Esta columna puede combinarse con la columna service_contract_id de sys.service_contracts. Acepta valores NULL.|  
|local_service_id|**int**|El identificador del servicio que se especifica como servicio local para la prioridad de conversación. Esta columna puede combinarse con la columna service_id de sys.services. Acepta valores NULL.|  
|remote_service_name|**nvarchar(256)**|El nombre del servicio que se especifica como servicio remoto para la prioridad de conversación. Acepta valores NULL.|  
|priority|**tinyint**|El nivel de prioridad que se especifica en esta prioridad de conversación. No acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se enumeran las prioridades de conversación utilizando combinaciones para mostrar los nombres del servicio local y del contrato.  
  
```  
SELECT scp.name AS priority_name,  
       ssc.name AS contract_name,  
       ssvc.name AS local_service_name,  
       scp.remote_service_name,  
       scp.priority AS priority_level  
FROM sys.conversation_priorities AS scp  
    INNER JOIN sys.service_contracts AS ssc  
       ON scp.service_contract_id = ssc.service_contract_id  
    INNER JOIN sys.services AS ssvc  
       ON scp.local_service_id = ssvc.service_id  
ORDER BY priority_name, contract_name,  
         local_service_name, remote_service_name;  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER BROKEr PRIORity &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKEr PRIORity &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [Sys. Services &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-services-transact-sql.md)   
 [Sys. service_contracts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-contracts-transact-sql.md)  
  
  
