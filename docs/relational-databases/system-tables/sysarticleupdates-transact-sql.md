---
title: sysarticleupdates (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2074e8fa160d2922bc67b5ef0167ace1328e6957
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada artículo que admite suscripciones de actualización inmediata. Esta tabla se almacena en la base de datos replicada.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Columna de identidad que proporciona un número de Id. único para el artículo.|  
|**pubid**|**int**|Id. de la publicación a la que pertenece el artículo.|  
|**sync_ins_proc**|**int**|Id. del procedimiento almacenado que controla las transacciones Insert Sync.|  
|**sync_upd_proc**|**int**|Id. del procedimiento almacenado que controla las transacciones Update Sync.|  
|**sync_del_proc**|**int**|Id. del procedimiento almacenado que controla las transacciones Delete Sync.|  
|**autogen**|**bit**|Indica que los procedimientos almacenados se generan automáticamente:<br /><br /> **0** = false, no automático.<br /><br /> **1** = true, automático.|  
|**sync_upd_trig**|**int**|Id. del desencadenador de versión automática en la tabla del artículo.|  
|**conflict_tableid**|**int**|Id. de la tabla de conflictos.|  
|**ins_conflict_proc**|**int**|El Id. del procedimiento utilizado para escribir el conflicto en la **conflict_table**.|  
|**identity_support**|**bit**|Especifica si está habilitada la administración automática de intervalos de identidad cuando se utiliza la actualización en cola. **0** significa que no hay ninguna identidad de intervalo de soporte técnico.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
