---
title: "Lección 2: Creación de una suscripción a la publicación transaccional | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54dd4030aa4212f23b1ccaf3f5b3a19ca8fc0f48
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lección 2: Crear una suscripción a la publicación transaccional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta lección, creará una suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para realizar esta lección es necesario haber completado la lección anterior, [Lección 1: Publicar datos con la replicación transaccional](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para crear la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en la publicación **AdvWorksProductTrans** y, después, haga clic en **Nuevas suscripciones**.  
  
    Se iniciará el Asistente para nueva suscripción.  
  
3.  En la página Publicación, seleccione **AdvWorksProductTrans**y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página Ubicación del Agente de distribución, seleccione **Ejecutar todos los agentes en el distribuidor**y luego haga clic en **Siguiente**.  
  
5.  En la página Suscriptores, si no se muestra el nombre de la instancia del suscriptor, haga clic en **Agregar suscriptor**y luego, en **Agregar suscriptor de SQL Server**, y escriba el nombre de la instancia del suscriptor en el cuadro de diálogo **Conectar al servidor** y, a continuación, haga clic en **Conectar**.  
  
6.  En la página Suscriptores, seleccione el nombre de instancia del servidor del suscriptor y luego seleccione **<New Database>** en **Base de datos de suscripciones**.  
  
7.  En el cuadro de diálogo **Nueva base de datos** , escriba **ProductReplica** en el cuadro **Nombre de la base de datos** , haga clic en **Aceptar**y luego, en **Siguiente**.  
  
8.  En el cuadro de diálogo **Seguridad del Agente de distribución**, haga clic en el botón de puntos suspensivos (**…**), escriba \<*Nombre_De_Equipo>***\repl_distribution** en el cuadro **Cuenta de proceso**, escriba la contraseña para esta cuenta, haga clic en **Aceptar** y luego en **Siguiente**.  
  
9. Haga clic en **Finalizar** para aceptar los valores predeterminados en las páginas restantes y finalizar el asistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Establecer permisos de base de datos en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Bases de datos**, **ProductReplica**y **Seguridad**, haga clic con el botón derecho en **Usuarios**y, después, seleccione **Nuevo usuario**.  
  
2.  En la página **General** , en la lista **Tipo de usuario** , seleccione **Usuario de Windows**.  
  
3.  Seleccione el cuadro **Nombre de usuario** y haga clic en el botón de puntos suspensivos, en el cuadro **Escriba el nombre del objeto que quiere seleccionar** escriba <nombre_equipo>**\repl_distribution**, haga clic en **Comprobar nombres** y luego en **Aceptar**.  
  
4.  En la página **Pertenencia**, en el área **Pertenencia al rol de la base de datos**, seleccione **db_owner** y haga clic en **Aceptar** para crear el usuario.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para ver el estado de sincronización de la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , expanda la publicación **AdvWorksProductTrans** , haga clic con el botón derecho en la suscripción de la base de datos **ProductReplica** y, después, haga clic en **Ver estado de sincronización**.  
  
    Se mostrará el actual estado de sincronización de la suscripción.  
  
3.  Si la suscripción no está visible en **AdvWorksProductTrans**, presione F5 para actualizar la lista.  
  
## <a name="next-steps"></a>Next Steps  
Ha creado correctamente una suscripción a la publicación transaccional. Dado que el Agente de distribución para esta suscripción se ejecuta continuamente, la suscripción se inicializa cuando se crea. A continuación, utilizará testigos de seguimiento para comprobar que los cambios se replican en el suscriptor y para determinar la latencia. Vea [Lesson 3: Validating the Subscription and Measuring Latency](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Ver también  
[Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)  
[Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
