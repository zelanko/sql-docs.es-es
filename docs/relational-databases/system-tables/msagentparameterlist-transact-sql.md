---
title: MSagentparameterlist (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs: TSQL
helpviewer_keywords: Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 60f13f390ec499a3cc6f8add79538ea6d2cb133d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSagentparameterlist** tabla contiene información de parámetros de agente de replicación y se utiliza para especificar los parámetros que se pueden establecer para un tipo de agente determinado. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|El tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = Agente lector del registro.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.<br /><br /> **9** = agente de lectura de cola.|  
|**parameter_name**|**sysname**|Nombre de un parámetro de agente válido.|  
|**valor predeterminado**|**nvarchar(4000)**|Valor predeterminado del parámetro del agente, donde NULL indica que no existe tal valor.|  
|**MIN_VALUE**|**int**|Establece un límite inferior para el parámetro del agente, donde NULL indica que no hay límite inferior.|  
|**MAX_VALUE**|**int**|Establece un límite superior para el parámetro del agente, donde NULL indica que no hay límite superior.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
