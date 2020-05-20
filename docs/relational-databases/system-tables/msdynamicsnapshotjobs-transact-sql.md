---
title: MSdynamicsnapshotjobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f717d5cf35349dcb99ec2022c5c0c92df5ea4286
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812814"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSdynamicsnapshotjobs** realiza un seguimiento de la información de filtro de fila con parámetros aplicada para generar una instantánea de datos filtrados. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. del trabajo de instantáneas de datos filtrados.|  
|**name**|**sysname**|Nombre del trabajo de instantáneas de datos filtrados.|  
|**pubid**|**uniqueidentifier**|Número de identificación único para esta publicación.|  
|**job_id**|**uniqueidentifier**|Id. del trabajo del Agente SQL Server en el distribuidor.|  
|**agent_id**|**int**|Id. del Agente SQL Server.|  
|**dynamic_filter_login**|**sysname**|Valor utilizado para evaluar la función de [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) en los filtros de fila con parámetros definidos para la publicación.|  
|**dynamic_filter_hostname**|**sysname**|Valor utilizado para evaluar la función de [host_name](../../t-sql/functions/host-name-transact-sql.md) en los filtros de fila con parámetros definidos para la publicación.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Ruta de acceso a la carpeta desde donde se leen los archivos de instantáneas si se utiliza una instantánea de datos filtrados.|  
|**partition_id**|**int**|Id. de la partición de datos a la que pertenece el trabajo.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
