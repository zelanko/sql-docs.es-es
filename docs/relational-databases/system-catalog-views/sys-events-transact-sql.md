---
title: Sys.Events (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a8c0bf976f87b2d5c2d5ba7a4a616240bbdd58bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada evento para el que se activa un desencadenador o una notificación de eventos. Estos eventos representan los tipos de evento que se especifican cuando se crea la notificación de eventos o desencadenador mediante [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) o [CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID del desencadenador o de la notificación de eventos. Este valor, junto con **tipo**, de forma única identifica la fila.|  
|**Tipo**|**int**|Evento que provoca la activación del desencadenador.|  
|**type_desc**|**nvarchar(60)**|Descripción del evento que provoca la activación del desencadenador.|  
|**is_trigger_event**|**bit**|1 = Evento de desencadenador.<br /><br /> 0 = Evento de notificación.|  
|**event_group_type**|**int**|Grupo de eventos donde se crea el desencadenador o la notificación de eventos o NULL si no se crea en un grupo de eventos.|  
|**event_group_type_desc**|**nvarchar(60)**|Descripción del grupo de eventos donde se crea el desencadenador o la notificación de eventos o NULL si no se crea en un grupo de eventos.|  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
