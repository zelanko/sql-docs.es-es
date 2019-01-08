---
title: MSrepl_queuedtraninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: debe88da4effd02ac15af965656232d4ec1f3395
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795497"
---
# <a name="msreplqueuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplication_queuedtraninfo** tabla se utiliza el proceso de replicación para almacenar información acerca de los comandos en cola emitidos por todas las suscripciones de actualización en cola que utilizan la actualización en cola basadas en SQL. Esta tabla se almacena en la base de datos de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|El nombre del publicador.|  
|**publisher_db**|**sysname**|El nombre de la base de datos de publicación.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**transacción**|**sysname**|Id. de transacción bajo el que se ha ejecutado el comando en cola.|  
|**maxorderkey**|**bigint**|Solo para uso interno.|  
|**commandcount**|**bigint**|Solo para uso interno.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
