---
title: "Propiedades de la suscripción: publicador | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.subproperties.publisher.f1
helpviewer_keywords: Subscription Properties dialog box
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e23aa71ea138af1689a60a44f00424a4158906c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="subscription-properties---publisher"></a>Propiedades de la suscripción: publicador
  El cuadro de diálogo **Propiedades de la suscripción** del publicador permite ver y definir las propiedades para las suscripciones de inserción. También se pueden ver algunas propiedades para las suscripciones de extracción, pero el cuadro de diálogo **Propiedades de la suscripción** del suscriptor muestra propiedades adicionales y permite modificarlas.  
  
 Cada una de las propiedades del cuadro de diálogo **Propiedades de la suscripción** incluye una descripción. Haga clic en una propiedad para mostrar la descripción en la parte inferior del cuadro de diálogo. Este tema proporciona información adicional sobre una serie de propiedades, la mayoría de las cuales se muestran en el publicador únicamente para las suscripciones de inserción. Las propiedades se agrupan en las siguientes categorías:  
  
-   Propiedades que se aplican a todas las suscripciones.  
  
-   Propiedades que se aplican a las suscripciones transaccionales.  
  
-   Propiedades que se aplican a las suscripciones de mezcla.  
  
 Si una opción se muestra como de solo lectura, solamente se puede establecer durante la creación de la suscripción. Si desea establecer opciones que no están disponibles en el Asistente para nueva suscripción, cree la suscripción con los procedimientos almacenados. Para obtener más información, consulte [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) y [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md).  
  
## <a name="options-for-all-subscriptions"></a>Opciones para todas las suscripciones  
 **Seguridad**  
 Haga clic en la fila **Cuenta de proceso del agente** y, a continuación, haga clic en el botón de propiedades (**...**) para cambiar la cuenta con la que el Agente de distribución o el Agente de mezcla se ejecutan en el distribuidor. Para cambiar la cuenta en la que el Agente de distribución o el Agente de mezcla realizan conexiones al suscriptor, haga clic en **Conexión de suscriptor**y, a continuación, haga clic en el botón de propiedades (**…**).  
  
 Para obtener más información acerca de los permisos necesarios para cada agente, vea [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="options-for-transactional-subscriptions"></a>Opciones para suscripciones transaccionales  
 **Impedir bucles de transacciones**  
 Determina si el agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor. Esta opción se utiliza para la replicación transaccional bidireccional. Para más información, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).  
  
 **Suscripción actualizable**  
 Determina si los cambios del suscriptor se vuelven a replicar en el publicador. Es posible replicar los cambios con una actualización en cola o una actualización inmediata. La opción **Método de actualización del suscriptor** determina el método que se debe utilizar. Para más información, consulte [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
## <a name="options-for-merge-subscriptions"></a>Opciones para suscripciones de mezcla  
 **Definición de partición (HOST_NAME)**  
 Para una publicación que utiliza filtros con parámetros, la replicación de mezcla evalúa una de las dos funciones del sistema (o ambas si el filtro hace referencia a las dos) durante la sincronización para determinar los datos que un suscriptor debe recibir: **SUSER_SNAME()** o **HOST_NAME()**. De manera predeterminada, **HOST_NAME()** devuelve el nombre del equipo en el que se ejecuta el Agente de mezcla, pero puede reemplazar este valor en el Asistente para nueva suscripción. Para obtener más información acerca de los filtros con parámetros y de cómo reemplazar **HOST_NAME()**, vea [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 **Tipo de suscripción** y **Prioridad**  
 Muestra si la suscripción es una suscripción de cliente o de servidor (no podrá cambiarse una vez creada la suscripción). Las suscripciones de servidor pueden volver a publicar datos en otros suscriptores y es posible asignarles una prioridad para la resolución de conflictos.  
  
 Si ha seleccionado un tipo de suscripción de servidor en el Asistente para nueva suscripción, el suscriptor recibe la prioridad que se utiliza durante la resolución de conflictos.  
  
 **Solucionar conflictos de manera interactiva**  
 Establece si se va a utilizar la interfaz de usuario Solucionador interactivo para solucionar conflictos durante la sincronización de mezcla. Requiere un valor de **Habilitado** en **Utilizar el Administrador de sincronización de Windows**. Para obtener más información, consulte [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
