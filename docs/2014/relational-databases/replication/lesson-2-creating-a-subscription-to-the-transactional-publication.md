---
title: 'Lección 2: Crear una suscripción a la publicación transaccional | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d3e8b5f0be58d9153fbe4d0ffd0287ea753fcc5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721077"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lección 2: Crear una suscripción a la publicación transaccional
  En esta lección, creará una suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Esta lección es necesario que haya completado la lección anterior, [lección 1: Publicación de datos con la replicación transaccional](lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para crear la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en la publicación **AdvWorksProductTrans** y, después, haga clic en **Nuevas suscripciones**.  
  
     Se iniciará el Asistente para nueva suscripción.  
  
3.  En la página Publicación, seleccione **AdvWorksProductTrans**y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página Ubicación del Agente de distribución, seleccione **Ejecutar todos los agentes en el distribuidor**y luego haga clic en **Siguiente**.  
  
5.  En la página Suscriptores, si no se muestra el nombre de la instancia del suscriptor, haga clic en **Agregar suscriptor**y luego, en **Agregar suscriptor de SQL Server**, y escriba el nombre de la instancia del suscriptor en el cuadro de diálogo **Conectar al servidor** y, a continuación, haga clic en **Conectar**.  
  
6.  En la página suscriptores, seleccione el nombre de instancia del servidor del suscriptor y seleccione  **\<nueva base de datos >** en **base de datos de suscripción**.  
  
7.  En el cuadro de diálogo **Nueva base de datos** , escriba **ProductReplica** en el cuadro **Nombre de la base de datos** , haga clic en **Aceptar**y luego, en **Siguiente**.  
  
8.  En el **seguridad del agente de distribución** diálogo cuadro, haga clic en el botón de puntos suspensivos ( **...** ) botón, escriba \< _nombre_equipo >_ **\repl_distribution** en el **cuenta de proceso** , escriba la contraseña para este cuenta y, a continuación, haga clic en **Aceptar**y, a continuación, haga clic en **siguiente**.  
  
9. Haga clic en **Finalizar** para aceptar los valores predeterminados en las páginas restantes y finalizar el asistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Establecer permisos de base de datos en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Bases de datos**, **ProductReplica**y **Seguridad**, haga clic con el botón derecho en **Usuarios**y, después, seleccione **Nuevo usuario**.  
  
2.  En la página **General** , en la lista **Tipo de usuario** , seleccione **Usuario de Windows**.  
  
3.  Seleccione el **nombre de usuario** cuadro y haga clic en el botón de puntos suspensivos (...), en el **escriba el nombre de objeto a seleccionar** cuadro, escriba < nombre_equipo > **\repl_distribution**, haga clic en  **Comprobar nombres**y, a continuación, haga clic en **Aceptar**.  
  
4.  En la página **Pertenencia** , en el área **Pertenencia al rol de la base de datos** , seleccione **db_owner**y haga clic en **Aceptar** para crear el usuario.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para ver el estado de sincronización de la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , expanda la publicación **AdvWorksProductTrans** , haga clic con el botón derecho en la suscripción de la base de datos **ProductReplica** y, después, haga clic en **Ver estado de sincronización**.  
  
     Se mostrará el actual estado de sincronización de la suscripción.  
  
3.  Si la suscripción no está visible en **AdvWorksProductTrans**, presione F5 para actualizar la lista.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha creado correctamente una suscripción a la publicación transaccional. Dado que el Agente de distribución para esta suscripción se ejecuta continuamente, la suscripción se inicializa cuando se crea. A continuación, utilizará testigos de seguimiento para comprobar que los cambios se replican en el suscriptor y para determinar la latencia. Consulte [Lección 3: Validación de la suscripción y medir la latencia](lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Suscribirse a publicaciones](subscribe-to-publications.md)  
  
  
