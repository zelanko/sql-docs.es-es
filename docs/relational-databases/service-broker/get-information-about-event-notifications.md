---
title: "Obtener información sobre notificaciones de eventos | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6e41d81ae5f32fd8d78e1515f17a9229129348df
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="get-information-about-event-notifications"></a>Obtener información sobre notificaciones de eventos
  A continuación se indican las vistas de catálogo que están disponibles para consultar metadatos acerca de las notificaciones de eventos.  
  
 **Para obtener información acerca de notificaciones de eventos que no tengan lugar en servidores**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Para ver los metadatos de cualquier notificación de eventos de **sys.event_notifications** creada en bases de datos, como mínimo debe tener el permiso CONTROL, ALTER, TAKE OWNERSHIP o VIEW DEFINITION en la base de datos, ser el propietario de la notificación de eventos o tener el permiso ALTER ANY DATABASE EVENT NOTIFICATION. Para las notificaciones de eventos creadas en una cola específica, como mínimo debe tener el permiso CONTROL, ALTER, TAKE OWNERSHIP o VIEW DEFINITION en el objeto, ser el propietario de la notificación de eventos o tener el permiso ALTER ANY DATABASE EVENT NOTIFICATION.  
  
 **Para obtener información acerca de notificaciones de eventos que tienen lugar en servidores**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  Como mínimo requiere el permiso CONTROL o VIEW ANY DEFINITION en el servidor, ser el inicio de sesión o propietario de la notificación de eventos, o bien tener el permiso ALTER ANY EVENT NOTIFICATION para ver los metadatos de cualquier notificación de eventos de **sys.server_event_notifications**.  
  
 **Para obtener información acerca de todos los eventos que pueden desencadenar notificaciones de eventos**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  Esta vista de catálogo no devuelve grupos de eventos.  
  
## <a name="see-also"></a>Vea también  
 [Notificaciones de eventos](../../relational-databases/service-broker/event-notifications.md)  
  
  
