---
title: "Lecci&#243;n 3: Sincronizar la suscripci&#243;n con la publicaci&#243;n de combinaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicación [SQL Server], tutoriales"
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Lecci&#243;n 3: Sincronizar la suscripci&#243;n con la publicaci&#243;n de combinaci&#243;n
En esta lección iniciará el Agente de mezcla para inicializar la suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. También utilizará este procedimiento para sincronizar con el publicador. Esta lección requiere que haya completado la lección anterior, [Lección 2: Crear una suscripción a la publicación de mezcla](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### Para iniciar la sincronización e inicializar la suscripción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación**.  
  
2.  En la carpeta **Suscripciones locales**, haga clic con el botón derecho en la suscripción de la base de datos **SalesOrdersReplica** y, después, haga clic en **Ver estado de sincronización**.  
  
3.  Haga clic en **Inicio** para inicializar la suscripción.  
  
## Pasos siguientes  
Ha ejecutado correctamente el Agente de mezcla para iniciar la sincronización e inicializar la suscripción. También puede insertar, actualizar o eliminar datos en las tablas **SalesOrderHeader** o **SalesOrderDetail** en el publicador o en el suscriptor, repetir este procedimiento cuando exista conectividad de red para sincronizar datos entre el publicador y el suscriptor y, después, consultar las tablas **SalesOrderHeader** o **SalesOrderDetail** en el otro servidor para ver los cambios replicados.  
  
Con esto finaliza el tutorial Replicar datos con clientes móviles. Para obtener un tutorial similar que usa la replicación transaccional, consulte [Tutorial: Replicar datos entre servidores conectados de forma continua](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## Vea también  
[Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Sincronizar datos](../../relational-databases/replication/synchronize-data.md)  
[Sincronizar una suscripción de extracción](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
