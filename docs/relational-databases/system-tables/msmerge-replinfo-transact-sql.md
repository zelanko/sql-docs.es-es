---
description: MSmerge_replinfo (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce4bee70ea5ef410512ce399e8d715fbc321e1a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545617"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSmerge_replinfo** contiene una fila por cada suscripción. En esta tabla se hace un seguimiento de la información acerca de las suscripciones. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|Id. único de la réplica.|  
|**use_interactive_resolver**|**bit**|Especifica si se utiliza el solucionador interactivo durante la reconciliación.<br /><br /> **0** = no se utiliza el solucionador interactivo.<br /><br /> **1** = usar el solucionador interactivo.|  
|**validation_level**|**int**|Tipo de validación que se llevará a cabo en la suscripción. El nivel de validación especificado puede ser uno de estos valores:<br /><br /> **0** = sin validación.<br /><br /> **1** = validación solo del recuento de filas.<br /><br /> **2** = recuento de filas y validación de suma de comprobación.<br /><br /> **3** = recuento de filas y validación de suma de comprobación binaria.|  
|**resync_gen**|**bigint**|El número de generación que se utiliza para volver a sincronizar la suscripción. Un valor de **-1** indica que la suscripción no está marcada para resincronización.|  
|**login_name**|**sysname**|Nombre del usuario que creó la suscripción.|  
|**hostname**|**sysname**|El valor que utiliza el filtro de fila con parámetros al generar la partición de la suscripción.|  
|**merge_jobid**|**binario (16)**|Id. de trabajo de mezcla para esta suscripción.|  
|**sync_info**|**int**|Solo para uso interno.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
