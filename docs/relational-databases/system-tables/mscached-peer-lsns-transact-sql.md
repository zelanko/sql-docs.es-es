---
description: MScached_peer_lsns (Transact-SQL)
title: MScached_peer_lsns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 23d4339d7a907cd755934df4803e38f5ba769b5e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551020"
---
# <a name="mscached_peer_lsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MScached_peer_lsns** se utiliza para realizar el seguimiento de los valores de LSN del registro de transacciones que se utilizan para determinar qué comandos se van a devolver a un suscriptor determinado en la replicación punto a punto. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Id. del Agente de distribución.|  
|**llegar**|**sysname**|Nombre del publicador de origen.|  
|**originator_db**|**sysname**|Nombre de la base de datos de publicación de origen.|  
|**originator_publication_id**|**int**|Identifica la publicación de origen.|  
|**originator_db_version**|**int**|Identifica el número de versión de la base de datos de origen.|  
|**originator_lsn**|**varbinary(16)**|LSN de la transacción de origen.|  
  
## <a name="remarks"></a>Observaciones  
 Los valores de LSN solo se utilizan inmediatamente después de la inserción, y no tienen un significado duradero en el sistema.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
