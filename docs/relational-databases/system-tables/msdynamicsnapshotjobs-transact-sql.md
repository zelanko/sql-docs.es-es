---
title: MSdynamicsnapshotjobs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs: TSQL
helpviewer_keywords: MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79f353d2c95f9e7c9c8071de60bb8c2705f675b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdynamicsnapshotjobs** tabla realiza un seguimiento de la información de filtro de fila con parámetros aplicada para generar una instantánea de datos filtrados. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del trabajo de instantáneas de datos filtrados.|  
|**Nombre**|**sysname**|El nombre del trabajo de instantáneas de datos filtrados.|  
|**pubid**|**uniqueidentifier**|Número de identificación único para esta publicación.|  
|**job_id**|**uniqueidentifier**|El identificador del trabajo de agente SQL Server en el distribuidor.|  
|**agent_id**|**int**|El identificador del Agente SQL Server.|  
|**dynamic_filter_login**|**sysname**|El valor utilizado para evaluar la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) función en filtros de fila con parámetros definidos para la publicación.|  
|**dynamic_filter_hostname**|**sysname**|El valor utilizado para evaluar la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función en filtros de fila con parámetros definidos para la publicación.|  
|**ubicacióndeinstantáneadinámica**|**nvarchar(255)**|Ruta de acceso a la carpeta desde donde se leen los archivos de instantáneas si se utiliza una instantánea de datos filtrados.|  
|**partition_id**|**int**|Id. de la partición de datos a la que pertenece el trabajo.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
