---
title: 'Lección 3: Sincronización de la suscripción con la publicación de combinación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: af7e1e4c59cfc624e9e83a24fcbb6095a20d2dda
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114014"
---
# <a name="lesson-3-synchronizing-the-subscription-to-the-merge-publication"></a>Lección 3: Sincronizar la suscripción con la publicación de combinación
  En esta lección iniciará el Agente de mezcla para inicializar la suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. También utilizará este procedimiento para sincronizar con el publicador. Esta lección requiere que haya completado la lección anterior, [Lección 2: Crear una suscripción a la publicación de mezcla](lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>Para iniciar la sincronización e inicializar la suscripción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Suscripciones locales** , haga clic con el botón derecho en la suscripción de la base de datos **SalesOrdersReplica** y, después, haga clic en **Ver estado de sincronización**.  
  
3.  Haga clic en **Inicio** para inicializar la suscripción.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha ejecutado correctamente el Agente de mezcla para iniciar la sincronización e inicializar la suscripción. También puede insertar, actualizar o eliminar datos en las tablas **SalesOrderHeader** o **SalesOrderDetail** en el publicador o en el suscriptor, repetir este procedimiento cuando exista conectividad de red para sincronizar datos entre el publicador y el suscriptor y, después, consultar las tablas **SalesOrderHeader** o **SalesOrderDetail** en el otro servidor para ver los cambios replicados.  
  
 Con esto finaliza el tutorial Replicar datos con clientes móviles. Para obtener un tutorial similar que usa la replicación transaccional, consulte [Tutorial: Replicar datos entre servidores conectados de forma continua](tutorial-replicating-data-between-continuously-connected-servers.md).  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Synchronize Data](synchronize-data.md)  (Sincronizar datos)  
 [Sincronizar una suscripción de extracción](synchronize-a-pull-subscription.md)  
  
  