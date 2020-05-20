---
title: 'Lección 2: Creación de una suscripción a la publicación transaccional | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9dc9824efb3f962d97f786835fa2367be18b55f7
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000419"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lección 2: Crear una suscripción a la publicación transaccional
  En esta lección, creará una suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para realizar esta lección es necesario haber completado la lección anterior, [Lección 1: Publicar datos con la replicación transaccional](lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para crear la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en la publicación **AdvWorksProductTrans** y, después, haga clic en **Nuevas suscripciones**.  
  
     Se iniciará el Asistente para nueva suscripción.  
  
3.  En la página Publicación, seleccione **AdvWorksProductTrans**y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página Ubicación del Agente de distribución, seleccione **Ejecutar todos los agentes en el distribuidor**y luego haga clic en **Siguiente**.  
  
5.  En la página Suscriptores, si no se muestra el nombre de la instancia del suscriptor, haga clic en **Agregar suscriptor**y luego, en **Agregar suscriptor de SQL Server**, y escriba el nombre de la instancia del suscriptor en el cuadro de diálogo **Conectar al servidor** y, a continuación, haga clic en **Conectar**.  
  
6.  En la página suscriptores, seleccione el nombre de instancia del servidor del suscriptor y seleccione ** \< nuevo>de base de datos** en base de datos de **suscripciones**.  
  
7.  En el cuadro de diálogo **Nueva base de datos** , escriba **ProductReplica** en el cuadro **Nombre de la base de datos** , haga clic en **Aceptar**y luego, en **Siguiente**.  
  
8.  En el cuadro de diálogo **seguridad de agente de distribución** , haga clic en el botón de puntos suspensivos (**...**), escriba \< _Machine_Name>_ **\ repl_distribution** en el cuadro **cuenta de proceso** , escriba la contraseña para esta cuenta, haga clic en **Aceptar**y, a continuación, haga clic en **siguiente**.  
  
9. Haga clic en **Finalizar** para aceptar los valores predeterminados en las páginas restantes y finalizar el asistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Establecer permisos de base de datos en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Bases de datos**, **ProductReplica**y **Seguridad**, haga clic con el botón derecho en **Usuarios**y, después, seleccione **Nuevo usuario**.  
  
2.  En la página **General** , en la lista **Tipo de usuario** , seleccione **Usuario de Windows**.  
  
3.  Seleccione el cuadro **nombre de usuario** y haga clic en el botón de puntos suspensivos (...) y, en el cuadro Escriba **el nombre de objeto que desea seleccionar** , escriba <Machine_Name>**\ Repl_distribution**, haga clic en **Comprobar nombres**y, a continuación, haga clic en **Aceptar**.  
  
4.  En la página **Pertenencia** , en el área **Pertenencia al rol de la base de datos** , seleccione **db_owner**y haga clic en **Aceptar** para crear el usuario.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para ver el estado de sincronización de la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , expanda la publicación **AdvWorksProductTrans** , haga clic con el botón derecho en la suscripción de la base de datos **ProductReplica** y, después, haga clic en **Ver estado de sincronización**.  
  
     Se mostrará el actual estado de sincronización de la suscripción.  
  
3.  Si la suscripción no está visible en **AdvWorksProductTrans**, presione F5 para actualizar la lista.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha creado correctamente una suscripción a la publicación transaccional. Dado que el Agente de distribución para esta suscripción se ejecuta continuamente, la suscripción se inicializa cuando se crea. A continuación, utilizará testigos de seguimiento para comprobar que los cambios se replican en el suscriptor y para determinar la latencia. Vea [Lesson 3: Validating the Subscription and Measuring Latency](lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Consulte también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Crear una suscripción de extracción](create-a-push-subscription.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
