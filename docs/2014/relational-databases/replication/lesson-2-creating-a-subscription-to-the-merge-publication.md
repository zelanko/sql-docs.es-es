---
title: 'Lección 2: Creación de una suscripción a la publicación de combinación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a39b3395a26fdbe3c235f429f312f4d6b3aff512
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000446"
---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>Lección 2: Crear una suscripción a la publicación de combinación
  En esta lección, creará una suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Luego establecerá los permisos en la base de datos de suscripciones y generará manualmente la instantánea de datos filtrados para la nueva suscripción. Para realizar esta lección es necesario haber completado la lección anterior, [Lección 1: Publicar datos con la replicación de mezcla](lesson-1-publishing-data-using-merge-replication.md).  
  
### <a name="to-create-the-subscription"></a>Para crear la suscripción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor, expanda la carpeta **Replicación** , haga clic con el botón derecho en la carpeta **Suscripciones locales** y, después, haga clic en **Nueva suscripción**.  
  
     Se iniciará el Asistente para nueva suscripción.  
  
2.  En la página **Publicación** , haga clic en **Buscar publicador de SQL Server** en la lista **Publicador** .  
  
3.  En el cuadro de diálogo **Conectar al servidor** , escriba el nombre de la instancia del publicador en el cuadro **Nombre del servidor** y, después, haga clic en **Conectar**.  
  
4.  Haga clic en **AdvWorksSalesOrdersMerge**y en **Siguiente**.  
  
5.  En la página Ubicación del Agente de mezcla, haga clic en **Ejecutar cada agente en su suscriptor**y, luego, en **Siguiente**.  
  
6.  En la página suscriptores, seleccione el nombre de instancia del servidor del suscriptor y, en **base de datos de suscripciones**, seleccione ** \< nuevo>de base de datos** en la lista.  
  
7.  En el cuadro de diálogo **Nueva base de datos** , escriba **SalesOrdersReplica** en el cuadro **Nombre de la base de datos** , haga clic en **Aceptar**y, después, haga clic en **Siguiente**.  
  
8.  En la página seguridad de Agente de mezcla, haga clic en el botón de puntos suspensivos (**...**), escriba \< _Machine_Name>_ **\ Repl_merge** en el cuadro **cuenta de proceso** , proporcione la contraseña para esta cuenta, haga clic en **Aceptar**, haga clic en **siguiente**y, a continuación, haga clic en **siguiente** de nuevo.  
  
9. En la página Inicializar suscripciones, seleccione **En la primera sincronización** de la lista **Inicializar cuando** , haga clic en **Siguiente**y, después, otra vez en **Siguiente** .  
  
10. En la página valores de HOST_NAME, escriba un valor de `adventure-works\pamela0` en el cuadro de **host_name valor** y, a continuación, haga clic en **Finalizar**.  
  
11. Haga clic de nuevo en **Finalizar** y, una vez creada la suscripción, haga clic en **Cerrar**.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Establecer permisos de base de datos en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Bases de datos**, **SalesOrdersReplica**y **Seguridad**, haga clic con el botón derecho en **Usuarios**y, después, seleccione **Nuevo usuario**.  
  
2.  En la **página general** , escriba \< _Machine_Name>_ **\ Repl_merge** en el cuadro **nombre de usuario** , haga clic en el botón de puntos suspensivos (**...**), haga clic en **examinar**, seleccione \< _Machine_Name>repl_merge _ **\repl_merge**, haga clic en **Aceptar**, haga clic en **Comprobar nombres**y, a continuación, haga clic en **Aceptar**.  
  
3.  En **Pertenencia al rol de la base de datos**, seleccione **db_owner**y haga clic en **Aceptar** para crear el usuario.  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>Para crear la instantánea de datos filtrados para la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en la publicación **AdvWorksSalesOrdersMerge** y, luego, haga clic en **Propiedades**.  
  
     Se mostrará el cuadro de diálogo **Propiedades de la publicación** .  
  
3.  Seleccione la página **Particiones de datos** y haga clic en **Agregar**.  
  
4.  En el cuadro de diálogo **Agregar partición de datos** , escriba `adventure-works\pamela0` en el cuadro de **host_name valor** y, a continuación, haga clic en **Aceptar**.  
  
5.  Seleccione la partición agregada recientemente, haga clic en **Generar instantáneas seleccionadas ahora**y, después, haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha creado correctamente una suscripción a la publicación de combinación y ha generado la instantánea filtrada para la nueva partición de datos de la suscripción, de manera que esté disponible cuando se inicialice la suscripción. A continuación, concederá derechos al Agente de mezcla en la base de datos de suscripciones y ejecutará el Agente de mezcla para iniciar la sincronización e inicializar la suscripción. Vea [Lección 3: Sincronizar la suscripción con la publicación de combinación](lesson-3-synchronizing-the-subscription-to-the-merge-publication.md).  
  
## <a name="see-also"></a>Consulte también  
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Instantáneas para publicaciones de combinación con filtros con parámetros](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
