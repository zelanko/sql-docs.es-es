---
title: 'Lección 3: Sincronización de la suscripción con la publicación de combinación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 49008384-2c55-4080-a890-9bceb40e4d6d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 63d8f82d207a985bac34b5c9a9be3273bb84ef7d
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000399"
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
  
## <a name="see-also"></a>Consulte también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Sincronizar datos](synchronize-data.md)   
 [Sincronizar una suscripción de extracción](synchronize-a-pull-subscription.md)  
  
  
