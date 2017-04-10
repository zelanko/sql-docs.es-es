---
title: "Lecci&#243;n 3: Validar la suscripci&#243;n y medir la latencia | Microsoft Docs"
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
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Lecci&#243;n 3: Validar la suscripci&#243;n y medir la latencia
En esta lección, utilizará testigos de seguimiento para comprobar que los cambios se replican en el suscriptor y para determinar la latencia, es decir, el tiempo que se requiere para que un cambio realizado en el publicador aparezca en el suscriptor. Esta lección requiere que haya completado la lección anterior, [Lección 2: Crear una suscripción a la publicación transaccional](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
### Para insertar un testigo de seguimiento y ver la información del token  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor, haga clic con el botón derecho en la carpeta **Replicación** y luego en **Iniciar el Monitor de replicación**.  
  
    Se inicia el Monitor de replicación.  
  
2.  Expanda un grupo de publicador en el panel izquierdo, expanda una instancia de publicador y, a continuación, haga clic en la publicación **AdvWorksProductTrans** .  
  
3.  Haga clic en la pestaña **Testigos de seguimiento** .  
  
4.  Haga clic en **Insertar seguimiento**.  
  
5.  Vea el tiempo transcurrido para el testigo de seguimiento en las siguientes columnas: **Publicador a distribuidor**, **Distribuidor a suscriptor**y **Latencia total**. El valor **Pendiente** indica que el testigo no ha alcanzado un punto específico.  
  
## Pasos siguientes  
En esta lección, utilizó correctamente los testigos de seguimiento para comprobar que los cambios de datos se replican del publicador al suscriptor. También puede insertar, actualizar o eliminar datos en la tabla **Product** en el publicador y consultar la tabla **Product** en el suscriptor para ver esos cambios, una vez replicados.  
  
Con esto finaliza el tutorial Replicar datos entre servidores conectados de forma continua. Para realizar un tutorial similar que utiliza replicación de mezcla, vea [Tutorial: Replicating Data with Mobile Clients](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md).  
  
## Vea también  
[Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
  
