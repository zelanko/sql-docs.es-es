---
description: MSsnapshot_history (Transact-SQL)
title: MSsnapshot_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 803333fc2cd28c94005c33a909c990de598e232c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89524512"
---
# <a name="mssnapshot_history-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSsnapshot_history** contiene las filas de historial de los agentes de instantáneas asociados al distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Id. del Agente de instantáneas.|  
|**runstatus**|**int**|Estado de ejecución:<br /><br /> **1** = Inicio.<br /><br /> **2** = correcto.<br /><br /> **3** = en curso.<br /><br /> **4** = inactivo.<br /><br /> **5** = Reintentar.<br /><br /> **6** = error.|  
|**start_time**|**datetime**|Hora a la que comienza la ejecución del trabajo.|  
|**time**|**datetime**|Hora a la que se registra el mensaje.|  
|**duration**|**int**|Duración, en segundos, de la sesión del mensaje.|  
|**comentarios**|**nvarchar(255)**|Texto del mensaje.|  
|**delivered_transactions**|**int**|Número total de transacciones entregadas en la sesión.|  
|**delivered_commands**|**int**|Número de comandos entregados por segundo.|  
|**delivery_rate**|**float(53)**|Promedio de comandos entregados por segundo.|  
|**error_id**|**int**|IDENTIFICADOR del error en la [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) tabla del sistema.|  
|**timestamp**|**timestamp**|La columna de marca de tiempo de esta tabla.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
