---
title: "Inicializar suscripciones | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.initializesubscriptions.f1"
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Inicializar suscripciones
  Deberá inicializar los suscriptores antes de que puedan comenzar a recibir datos replicados. No se requiere un conjunto de datos inicial, pero el suscriptor deberá poseer al menos el esquema de cada objeto replicado y todas las tablas de metadatos y los procedimientos necesarios para la replicación.  
  
## Opciones  
 **Propiedades de la suscripción**  
 Active la casilla de verificación en la **inicializar** columna para cada suscriptor que requiere un conjunto de datos inicial. Si desactiva la casilla, solo se inicializarán los procedimientos y metadatos de replicación. Para obtener más información acerca de cómo inicializar una suscripción sin una instantánea, consulte [inicializar una suscripción transaccional sin una instantánea](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Seleccione **inmediatamente** en el cuadro de lista desplegable de la **inicializar cuando** columna para que el agente de mezcla o el agente de distribución transfiera archivos de instantáneas al suscriptor una vez finalizado el asistente. Seleccione **En la primera sincronización** para que el agente transfiera los archivos la próxima vez que esté programado para ejecutarse. La opción **Inmediatamente** no está disponible para suscripciones de extracción a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. El Agente de mezcla y el Agente de distribución no se ejecutarán con instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], por lo que deberá inicializar la suscripción de otra forma.  
  
> [!NOTE]  
>  El asistente podría solicitar una conexión al distribuidor para iniciar un trabajo adecuado del Agente de distribución o el Agente de mezcla.  
  
## Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Inicializar una suscripción](../../relational-databases/replication/initialize-a-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  