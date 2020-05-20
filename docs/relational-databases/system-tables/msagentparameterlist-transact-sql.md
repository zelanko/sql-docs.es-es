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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e82c9dd6bd2768e997e74508741d047d0155665f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832395"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSagentparameterlist** contiene información sobre los parámetros del agente de replicación y se usa para especificar los parámetros que se pueden establecer para un tipo de agente determinado. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|El tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = agente de registro del log.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.<br /><br /> **9** = agente de lectura de cola.|  
|**parameter_name**|**sysname**|Nombre de un parámetro de agente válido.|  
|**default_value**|**nvarchar(4000)**|Valor predeterminado del parámetro del agente, donde NULL indica que no existe tal valor.|  
|**min_value**|**int**|Establece un límite inferior para el parámetro del agente, donde NULL indica que no hay límite inferior.|  
|**max_value**|**int**|Establece un límite superior para el parámetro del agente, donde NULL indica que no hay límite superior.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
