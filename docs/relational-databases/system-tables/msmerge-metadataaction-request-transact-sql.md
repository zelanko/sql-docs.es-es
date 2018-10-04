---
title: MSmerge_metadataaction_request (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed94d3fc295ffdcac9d26b13525a79f782a0c9c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763753"
---
# <a name="msmergemetadataactionrequest-transact-sql"></a>MSmerge_metadataaction_request (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_metadataaction_request** tabla almacena una fila por cada acción de compensación necesaria. Usar sincronización Web, si se produce un error y se debe volver a intentar la sincronización, se realiza una entrada en **MSmerge_metadataaction_request**. Durante la fase de carga de la mezcla posterior, las solicitudes de todos los artículos pertenecientes a la publicación que se está sincronizando se recuperan de esta taba y se cargan. Cuando se haya completado correctamente la sincronización, la fila correspondiente en el **MSmerge_metadataaction_request** se elimina la tabla. Esta tabla se almacena en la base de datos de publicación del publicador y en la base de datos de suscripciones del suscriptor.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|El alias de la tabla publicada.|  
|**rowguid**|**uniqueidentifier**|Identificador de la fila especificada.|  
|**action**|**tinyint**|Identifica la acción de compensación necesaria.|  
|**generación**|**bigint**|El valor de la generación para la que se necesita la acción de compensación.|  
|**puede cambiar**|**int**|Solo para uso interno.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
