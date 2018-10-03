---
title: MSagentparameterlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
ms.openlocfilehash: 1a765732f4d44ef31ed947a10d3b9449e261d1a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47760933"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSagentparameterlist** tabla contiene información de parámetro del agente de replicación y se usa para especificar los parámetros que se pueden establecer para un tipo de agente determinado. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|El tipo de agente:<br /><br /> **1** = agente de instantáneas.<br /><br /> **2** = Agente lector del registro.<br /><br /> **3** = agente de distribución.<br /><br /> **4** = agente de mezcla.<br /><br /> **9** = agente de lector de cola.|  
|**parameter_name**|**sysname**|Nombre de un parámetro de agente válido.|  
|**default_value**|**nvarchar(4000)**|Valor predeterminado del parámetro del agente, donde NULL indica que no existe tal valor.|  
|**MIN_VALUE**|**int**|Establece un límite inferior para el parámetro del agente, donde NULL indica que no hay límite inferior.|  
|**MAX_VALUE**|**int**|Establece un límite superior para el parámetro del agente, donde NULL indica que no hay límite superior.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
