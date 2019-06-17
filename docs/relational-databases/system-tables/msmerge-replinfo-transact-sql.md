---
title: MSmerge_replinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cae6c84d0ca85a8cb27d8310bcc3cb02dca47f8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62903353"
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_replinfo** tabla contiene una fila por cada suscripción. En esta tabla se hace un seguimiento de la información acerca de las suscripciones. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|Id. único de la réplica.|  
|**use_interactive_resolver**|**bit**|Especifica si se utiliza el solucionador interactivo durante la reconciliación.<br /><br /> **0** = no no utiliza el solucionador interactivo.<br /><br /> **1** = utilice el solucionador interactivo.|  
|**validation_level**|**int**|Tipo de validación que se llevará a cabo en la suscripción. El nivel de validación especificado puede ser uno de estos valores:<br /><br /> **0** no = ninguna validación.<br /><br /> **1** = validación solo del recuento de filas.<br /><br /> **2** = validación del recuento de filas y suma de comprobación.<br /><br /> **3** = recuento de filas y validación de suma de comprobación binaria.|  
|**resync_gen**|**bigint**|El número de generación que se utiliza para volver a sincronizar la suscripción. Un valor de **-1** indica que la suscripción no está marcada para la resincronización.|  
|**login_name**|**sysname**|Nombre del usuario que creó la suscripción.|  
|**hostname**|**sysname**|El valor que utiliza el filtro de fila con parámetros al generar la partición de la suscripción.|  
|**merge_jobid**|**binary(16)**|Id. de trabajo de mezcla para esta suscripción.|  
|**sync_info**|**int**|Solo para uso interno.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
