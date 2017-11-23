---
title: MSmerge_metadataaction_request (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7cdb53489f18f2936a418e9a4a1d29145fcdb4ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_metadataaction_request** tabla incluye una fila para cada acción de compensación que se necesita. Usar sincronización Web, si se produce un error y debe volver a intentarse la sincronización, se realiza una entrada en **MSmerge_metadataaction_request**. Durante la fase de carga de la mezcla posterior, las solicitudes de todos los artículos pertenecientes a la publicación que se está sincronizando se recuperan de esta taba y se cargan. Cuando se ha completado correctamente la sincronización, la fila correspondiente en el **MSmerge_metadataaction_request** se elimina la tabla. Esta tabla se almacena en la base de datos de publicación del publicador y en la base de datos de suscripciones del suscriptor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|El alias de la tabla publicada.|  
|**ROWGUID**|**uniqueidentifier**|Identificador de la fila especificada.|  
|**acción**|**tinyint**|Identifica la acción de compensación necesaria.|  
|**generación**|**bigint**|El valor de la generación para la que se necesita la acción de compensación.|  
|**cambiado**|**int**|Solo para uso interno.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
