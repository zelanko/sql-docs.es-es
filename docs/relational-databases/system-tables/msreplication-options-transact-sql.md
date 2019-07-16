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
author: stevestein
ms.author: sstein
ms.openlocfilehash: c48a57b876cde41d6bb514c522bcaa241eec11fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063003"
---
# <a name="msreplicationoptions-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplication_options** tabla almacena los metadatos que se usan internamente para la replicación. Esta tabla se almacena en el **maestro** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Exclusivamente para uso interno.|  
|**value**|**bit**|Exclusivamente para uso interno.|  
|**major_version**|**int**|Exclusivamente para uso interno.|  
|**versión_secundaria**|**int**|Exclusivamente para uso interno.|  
|**revision**|**int**|Exclusivamente para uso interno.|  
|**install_failures**|**int**|Exclusivamente para uso interno.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
