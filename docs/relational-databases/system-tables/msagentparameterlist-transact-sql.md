---
title: MSagentparameterlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1fd8e84a443c87846b4c40c45152b1225e2bc7b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817091"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSagentparameterlist** tabla contiene información de parámetro del agente de replicación y se usa para especificar los parámetros que se pueden establecer para un tipo de agente determinado. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|El tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = Agente lector del registro.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.<br /><br /> **9** = agente de lector de cola.|  
|**parameter_name**|**sysname**|Nombre de un parámetro de agente válido.|  
|**default_value**|**nvarchar(4000)**|Valor predeterminado del parámetro del agente, donde NULL indica que no existe tal valor.|  
|**min_value**|**int**|Establece un límite inferior para el parámetro del agente, donde NULL indica que no hay límite inferior.|  
|**max_value**|**int**|Establece un límite superior para el parámetro del agente, donde NULL indica que no hay límite superior.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
