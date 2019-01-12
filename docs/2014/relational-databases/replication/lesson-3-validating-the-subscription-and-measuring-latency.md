---
title: 'Lección 3: Validación de la suscripción y medir la latencia | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 147f7b93-1804-4e0b-9e17-57a51d035b2a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 6968331bc7699334f61997ec6a16e521c158078a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54123976"
---
# <a name="lesson-3-validating-the-subscription-and-measuring-latency"></a>Lección 3: Validar la suscripción y medir la latencia
  En esta lección, utilizará testigos de seguimiento para comprobar que los cambios se replican en el suscriptor y para determinar la latencia, es decir, el tiempo que se requiere para que un cambio realizado en el publicador aparezca en el suscriptor. Esta lección es necesario que haya completado la lección anterior, [lección 2: Crear una suscripción a la publicación transaccional](lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>Para insertar un testigo de seguimiento y ver la información del token  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor, haga clic con el botón derecho en la carpeta **Replicación** y luego en **Iniciar el Monitor de replicación**.  
  
     Se inicia el Monitor de replicación.  
  
2.  Expanda un grupo de publicador en el panel izquierdo, expanda una instancia de publicador y, a continuación, haga clic en la publicación **AdvWorksProductTrans** .  
  
3.  Haga clic en la pestaña **Testigos de seguimiento** .  
  
4.  Haga clic en **Insertar seguimiento**.  
  
5.  Vea el tiempo transcurrido para el testigo de seguimiento en las siguientes columnas: **Publicador a distribuidor**, **distribuidor a suscriptor**, **latencia Total**. El valor **Pendiente** indica que el testigo no ha alcanzado un punto específico.  
  
## <a name="next-steps"></a>Pasos siguientes  
 En esta lección, utilizó correctamente los testigos de seguimiento para comprobar que los cambios de datos se replican del publicador al suscriptor. También puede insertar, actualizar o eliminar datos en la tabla **Product** en el publicador y consultar la tabla **Product** en el suscriptor para ver esos cambios, una vez replicados.  
  
 Con esto finaliza el tutorial Replicar datos entre servidores conectados de forma continua. Para ver un tutorial similar que utiliza la replicación de mezcla, vea [Tutorial: Replicar datos con clientes móviles](tutorial-replicating-data-with-mobile-clients.md).  
  
## <a name="see-also"></a>Vea también  
 [Medir la latencia y validar las conexiones de la replicación transaccional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
  
