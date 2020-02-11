---
title: MSqreader_agents (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_agents_TSQL
- MSqreader_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_agents system table
ms.assetid: dfa1f45e-c531-4385-a097-0a9edd1d7eab
author: stevestein
ms.author: sstein
ms.openlocfilehash: d032552769c32d691a526456cba68aec9ac397e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032574"
---
# <a name="msqreader_agents-transact-sql"></a>MSqreader_agents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSqreader_agents** contiene una fila por cada agente de lectura de cola que se ejecuta en el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**sesión**|**int**|El identificador del Agente de lectura de cola.|  
|**Name**|**nvarchar(100**|El nombre del Agente de lectura de cola.|  
|**job_id**|**binario (16)**|El número de ID. de trabajo único de la tabla **sysjobs** .|  
|**profile_id**|**int**|El ID. de Perfil de la tabla **MSagent_profiles** .|  
|**job_step_uid**|**uniqueidentifier**|El Id. único del paso de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se inicia el agente.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
