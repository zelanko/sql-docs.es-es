---
description: MSrepl_queuedtraninfo (Transact-SQL)
title: MSrepl_queuedtraninfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_queuedtraninfo_TSQL
- MSrepl_queuedtraninfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_queuedtraninfo system table
ms.assetid: af7a5baf-32ea-475f-b6b9-68c557b4980c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e95ac3bb96d726b1b02d0258f9364cc48a3af09d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480741"
---
# <a name="msrepl_queuedtraninfo-transact-sql"></a>MSrepl_queuedtraninfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  El proceso de replicación utiliza la tabla **MSreplication_queuedtraninfo** para almacenar información acerca de los comandos en cola emitidos por todas las suscripciones de actualización en cola que utilizan la actualización en cola basada en SQL. Esta tabla se almacena en la base de datos de suscripciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|El nombre del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos de publicación.|  
|**publicaciones**|**sysname**|Nombre de la publicación.|  
|**tranid**|**sysname**|Id. de transacción bajo el que se ha ejecutado el comando en cola.|  
|**maxorderkey**|**bigint**|Solo para uso interno.|  
|**commandcount**|**bigint**|Solo para uso interno.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
