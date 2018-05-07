---
title: MSagent_profiles (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 38afed73fdee3817e632c02a0584d960d589fe8d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="msagentprofiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSagent_profiles** tabla contiene una fila por cada perfil de agente de replicación definido. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|Id. de perfil.|  
|**profile_name**|**sysname**|Nombre de perfil único para el tipo de agente.|  
|**agent_type**|**int**|El tipo de agente:<br /><br /> **1** = agente de instantáneas<br /><br /> **2** = Agente lector del registro<br /><br /> **3** = agente de distribución<br /><br /> **4** = agente de mezcla<br /><br /> **9** = agente de lectura de cola|  
|**Tipo**|**int**|Tipo de perfil:<br /><br /> **0** = sistema**1** = personalizado|  
|**Descripción**|**nvarchar(3000)**|La descripción del perfil.|  
|**def_profile**|**bit**|Especifica si este perfil es el predeterminado para este tipo de agente.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
