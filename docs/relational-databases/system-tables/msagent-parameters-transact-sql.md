---
title: MSagent_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSagent_parameters_TSQL
- MSagent_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_parameters system table
ms.assetid: be30abc9-c00d-446f-b1b4-1269772f37e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cad69c92a58b9749008ceb1320076aa68665b90d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624414"
---
# <a name="msagentparameters-transact-sql"></a>MSagent_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSagent_parameters** tabla contiene los parámetros asociados a un perfil de agente. Los nombres de los parámetros son los mismos que los que admite el agente. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|El identificador del perfil desde el **MSagent_profiles** tabla.|  
|**parameter_name**|**sysname**|Nombre del parámetro.|  
|**Valor**|**nvarchar(255)**|El valor del parámetro.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
