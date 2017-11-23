---
title: MSsub_identity_range (Transact-SQL) | Documentos de Microsoft
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
- MSsub_identity_range_TSQL
- MSsub_identity_range
dev_langs: TSQL
helpviewer_keywords: MSsub_identity_range system table
ms.assetid: 26e20d28-14ed-44fc-af3b-4de386de4bb8
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06417c00191ad2a3002481c3b167e7305765acfd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssubidentityrange-transact-sql"></a>MSsub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSsub_identity_range** tabla proporciona soporte de administración de intervalo de identidad para las suscripciones. Esta tabla se almacena en las bases de datos de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**ObjID**|**int**|Identificador de la tabla cuya columna de identidad se administra mediante la replicación.|  
|**intervalo**|**bigint**|Controla el tamaño del intervalo de valores de identidad consecutivos que podrían asignarse al suscriptor en un ajuste.|  
|**last_seed**|**bigint**|Límite inferior del intervalo actual.|  
|**umbral**|**int**|Valor de porcentaje que controla cuándo el Agente de distribución asigna un nuevo intervalo de identidad. Cuando se especifica el porcentaje de valores en *umbral* es usa, el agente de distribución crea un nuevo intervalo de identidad.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
