---
title: "Propiedades de base de datos de distribuci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.distdbproperties.f1"
helpviewer_keywords: 
  - "Propiedades de base de datos de distribución, cuadro de diálogo"
ms.assetid: 0f404ab9-1237-4936-8df5-888baab6a245
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propiedades de base de datos de distribuci&#243;n
  El cuadro de diálogo **Propiedades de base de datos de distribución** permite ver un número de propiedades y establecer el período de retención de transacción y retención de historial para la base de datos.  
  
## Opciones  
 **Nombre**  
 Nombre de la base de datos de distribución que, de manera predeterminada, se establece 'distribución' (de solo lectura).  
  
 **Ubicaciones de archivos**  
 Ubicación del archivo de la base de datos y del archivo de registro (de solo lectura).  
  
 **Período de retención de transacción**  
 También se conoce como período de retención de distribución. Representa el tiempo durante el cual se almacenan las transacciones para la replicación transaccional. Para más información, consulte [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Período de retención del historial**  
 Representa el tiempo durante el cual se almacenan los metadatos de historial para todos los tipos de replicación.  
  
 **Seguridad del Agente de lectura de cola**  
 El Agente de lectura de cola se utiliza con la replicación transaccional que admite suscripciones de actualización en cola. El Agente de lectura de cola se crea automáticamente si selecciona **Publicación transaccional con suscripciones actualizables** en la página **Tipo de publicación** del Asistente para nueva publicación. Haga clic en **Configuración de seguridad…** para cambiar la cuenta con la que el agente se ejecuta y establece conexiones con el distribuidor.  
  
 También puede crearse un agente de lectura de cola seleccionando **Crear Agente de lectura de cola** en esta página (esta opción está deshabilitada si ya se ha creado el agente).  
  
 Puede encontrar más información de conexión para el Agente de lectura de cola en dos lugares:  
  
-   El agente se conecta al publicador con las credenciales especificadas en el cuadro de diálogo **Propiedades del publicador** , que se encuentra en la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor** .  
  
-   El agente se conecta con el suscriptor utilizando las credenciales especificadas para el Agente de distribución del Asistente para nueva suscripción.  
  
 Para obtener más información, consulte  \\[modelo de seguridad del agente de replicación](../Topic/Replication%20Agent%20Security%20Model.md).  
  
## Vea también  
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)   
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)   
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  