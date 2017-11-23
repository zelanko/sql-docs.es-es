---
title: MSmerge_replinfo (Transact-SQL) | Documentos de Microsoft
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
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs: TSQL
helpviewer_keywords: MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5dfda378d9d5327ab62803d07316c12e0eb9d3a9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_replinfo** tabla contiene una fila por cada suscripción. En esta tabla se hace un seguimiento de la información acerca de las suscripciones. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|Id. único de la réplica.|  
|**use_interactive_resolver**|**bit**|Especifica si se utiliza el solucionador interactivo durante la reconciliación.<br /><br /> **0** = no no utilizar el solucionador interactivo.<br /><br /> **1** = utilizar el solucionador interactivo.|  
|**validation_level**|**int**|Tipo de validación que se llevará a cabo en la suscripción. El nivel de validación especificado puede ser uno de estos valores:<br /><br /> **0** no = ninguna validación.<br /><br /> **1** = validación solo del recuento de filas.<br /><br /> **2** = validación del recuento de filas y suma de comprobación.<br /><br /> **3** = número de filas y validación de suma de comprobación binaria.|  
|**resync_gen**|**bigint**|El número de generación que se utiliza para volver a sincronizar la suscripción. Un valor de **-1** indica que la suscripción no está marcada para sincronizarse de nuevo.|  
|**login_name**|**sysname**|Nombre del usuario que creó la suscripción.|  
|**nombre de host**|**sysname**|El valor que utiliza el filtro de fila con parámetros al generar la partición de la suscripción.|  
|**merge_jobid**|**binary (16)**|Id. de trabajo de mezcla para esta suscripción.|  
|**sync_info**|**int**|Solo para uso interno.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
