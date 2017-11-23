---
title: MSdistributiondbs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- MSdistributiondbs_TSQL
- MSdistributiondbs
dev_langs: TSQL
helpviewer_keywords: MSdistributiondbs system table
ms.assetid: d7ffa9df-bf1d-41b8-837e-b762c17c2764
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0719a236dc200bed1cb46e7bc94bb1da478b5375
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msdistributiondbs-transact-sql"></a>MSdistributiondbs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdistributiondbs** tabla contiene una fila por cada base de datos de distribución definida en el distribuidor local. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|El nombre de la base de datos de distribución.|  
|**min_distretention**|**int**|El período mínimo de retención, en horas, antes de que se eliminen las transacciones.|  
|**max_distretention**|**int**|El período máximo de retención, en horas, antes de que se eliminen las transacciones.|  
|**history_retention**|**int**|El número de horas que se mantiene el historial.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
