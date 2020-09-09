---
description: MSmerge_history (Transact-SQL)
title: MSmerge_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 348df963920d35aeb874a83cad83701995d563cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540889"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSmerge_history** contiene filas de historial con descripciones detalladas de los resultados de las sesiones de trabajos de agente de mezcla anteriores. Esta tabla contiene una fila por cada línea de resultados del agente. Esta tabla se utiliza en la base de datos de distribución y en cada base de datos de suscripciones. En la base de datos de distribución, contiene el historial para todas las publicaciones de combinación y suscripciones que utilizan el Distribuidor. En cada base de datos de suscripciones, contiene el historial para las publicaciones a las que se suscribe el Suscriptor.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|El Id. del trabajo del Agente de mezcla.|  
|**agent_id**|**int**|El Id. del Agente de mezcla.|  
|**comentarios**|**nvarchar(255)**|Texto del mensaje.|  
|**error_id**|**int**|IDENTIFICADOR de un error en la tabla del sistema [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) .|  
|**timestamp**|**timestamp**|La columna de marca de tiempo de esta tabla.|  
|**updatable_row**|**bit**|Se establece en **1** si se puede sobrescribir la fila de historial.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
