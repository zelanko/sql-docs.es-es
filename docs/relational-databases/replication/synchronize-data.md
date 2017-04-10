---
title: "Sincronizar datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sincronización [replicación de SQL Server], acerca de sincronización"
  - "sincronización de replicación de mezcla [replicación de SQL Server]"
  - "scripts [replicación de SQL Server], sincronización y"
  - "sincronización [replicación de SQL Server]"
  - "replicación de instantáneas [SQL Server], sincronización"
  - "replicación transaccional, sincronización"
  - "suscripciones [replicación de SQL Server], sincronizar"
  - "ejecución a petición de script"
  - "replicación [SQL Server], sincronizar"
  - "scripts [replicación de SQL Server]"
ms.assetid: 724802f7-7d69-46d3-a330-bd8aa7f53114
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Sincronizar datos
  La sincronización de los datos se refiere al proceso de propagación de los cambios en los datos y el esquema entre el publicador y los suscriptores después de haber aplicado la instantánea inicial en el suscriptor. La sincronización puede producirse:  
  
-   De forma continua, lo que es típico de la replicación transaccional.  
  
-   A petición, lo que es típico de la replicación de mezcla.  
  
-   Según una programación, lo que es típico de la replicación de instantáneas.  
  
 Cuando se sincroniza una suscripción, se producen diferentes procesos según el tipo de replicación que se utilice:  
  
-   Replicación de instantáneas. La sincronización significa que el Agente de distribución vuelve a aplicar la instantánea en el suscriptor, de modo que los datos y el esquema de la base de datos de suscripciones sean coherentes con la base de datos de publicación.  
  
     Si se han realizado modificaciones de los datos o del esquema en el publicador, es necesario generar una nueva instantánea para poder propagarlas al suscriptor.  
  
-   Replicación transaccional. La sincronización significa que el Agente de distribución transfiere las actualizaciones, las inserciones, las eliminaciones y otros cambios de la base de datos de distribución al suscriptor.  
  
-   Replicación de mezcla. La sincronización significa que el Agente de mezcla carga los cambios del suscriptor en el publicador y, después, descarga los cambios del publicador en el suscriptor. Si hubiera conflictos, se detectan y se resuelven. Los datos convergen y, al final, el publicador y todos los suscriptores acaban por tener los mismos valores. Si se detectan conflictos y se resuelven, el trabajo confirmado por algunos usuarios se modifica para solucionar el conflicto según las directrices definidas.  
  
 Las publicaciones de instantáneas actualizan completamente el esquema en el suscriptor cada vez que se produce una sincronización, así que todos los cambios de esquema se aplican en el suscriptor. La replicación transaccional y la replicación de mezcla también admiten los cambios de esquema más comunes. Para obtener más información, consulte [hacer cambios de esquema en bases de datos de publicación](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Para sincronizar una suscripción de inserción, vea [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
 Para sincronizar una suscripción de extracción, vea [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
 Para establecer programaciones de sincronización, vea [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
 **Para ver y solucionar los conflictos de sincronización**  
  
-   [! INCLUIR [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [View and Resolve Data Conflicts for Merge Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)  
  
-   [! INCLUIR [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [View Data Conflicts for Transactional Publications &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
## Ejecutar código durante la sincronización  
 La replicación admite dos métodos de ejecución de código durante la sincronización  
  
-   La ejecución de script a petición se admite en la replicación transaccional y la replicación de mezcla. Con la ejecución de script a petición es posible especificar un script SQL para ejecutarlo durante la sincronización. Este script se copia en el suscriptor y se ejecuta mediante **sqlcmd** al inicio del proceso de sincronización. El script no tiene acceso a los cambios replicados cuando se aplican al suscriptor. Para obtener más información, consulte [Ejecutar Scripts durante la sincronización & #40; Programación de Transact-SQL de replicación & #41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   La replicación de mezcla admite controladores de lógica de negocios. El uso de un marco de trabajo de controladores de lógica de negocios le permite escribir un ensamblado de código administrado al que se llama durante el proceso de sincronización de mezcla. El ensamblado incluye lógica de negocios que puede responder a varias condiciones durante la sincronización: cambios de datos, conflictos y errores. Para obtener más información, consulte [ejecutar lógica de negocios durante la sincronización mezcla](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## Vea también  
 [Detectar y solucionar conflictos de replicación de mezcla](../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  