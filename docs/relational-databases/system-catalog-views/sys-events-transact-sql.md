---
title: Sys.Events (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cbe2fefe52f6a4254e0b8e9afb279f57e8b278bb
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43067775"
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada evento para el que se activa un desencadenador o una notificación de eventos. Estos eventos representan los tipos de evento que se especifican cuando se crea con la notificación de eventos o desencadenador [CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md) o [CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
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
  
  
