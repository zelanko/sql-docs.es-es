---
title: MSreplication_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8943c9e20e9c5add63cf9af21b3ac882696d01af
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757830"
---
# <a name="msreplication_options-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  En la tabla **MSreplication_options** se almacenan los metadatos que la replicación usa internamente. Esta tabla se almacena en la base de datos **maestra** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Exclusivamente para uso interno.|  
|**value**|**bit**|Exclusivamente para uso interno.|  
|**major_version**|**int**|Exclusivamente para uso interno.|  
|**minor_version**|**int**|Exclusivamente para uso interno.|  
|**revisión**|**int**|Exclusivamente para uso interno.|  
|**install_failures**|**int**|Exclusivamente para uso interno.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
