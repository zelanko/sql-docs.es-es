---
title: 'Lección 2: Creación de una suscripción a la publicación de combinación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7f1ab51a53e91a069e4d2a137d4908fa820df0f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186615"
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
  
6.  En la página suscriptores, seleccione el nombre de instancia del servidor del suscriptor y, en **base de datos de suscripción**, seleccione  **\<nueva base de datos >** en la lista.  
  
7.  En el cuadro de diálogo **Nueva base de datos** , escriba **SalesOrdersReplica** en el cuadro **Nombre de la base de datos** , haga clic en **Aceptar**y, después, haga clic en **Siguiente**.  
  
8.  En la página Seguridad del Agente de mezcla, haga clic en el botón de puntos suspensivos (**…**), escriba \<*Nombre_De_Equipo>***\repl_merge* en el cuadro **Cuenta de proceso**, escriba la contraseña de esta cuenta, haga clic en **Aceptar**, en **Siguiente** y, después, otra vez en **Siguiente**.  
  
9. En la página Inicializar suscripciones, seleccione **En la primera sincronización** de la lista **Inicializar cuando** , haga clic en **Siguiente**y, después, otra vez en **Siguiente** .  
  
10. En la página valores de HOST_NAME, escriba un valor de `adventure-works\pamela0` en el **valor de HOST_NAME** cuadro y, a continuación, haga clic en **finalizar**.  
  
11. Haga clic de nuevo en **Finalizar** y, una vez creada la suscripción, haga clic en **Cerrar**.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Establecer permisos de base de datos en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Bases de datos**, **SalesOrdersReplica**y **Seguridad**, haga clic con el botón derecho en **Usuarios**y, después, seleccione **Nuevo usuario**.  
  
2.  En la página **General**, escriba \<*Nombre_De_Equipo>***\repl_merge** en el cuadro **Nombre de usuario**, haga clic en el botón de puntos suspensivos (**…**), haga clic en **Examinar**, seleccione \<*Nombre_De_Equipo>***\repl_merge**, haga clic en **Aceptar**, en **Comprobar nombres** y luego en **Aceptar**.  
  
3.  En **Pertenencia al rol de la base de datos**, seleccione **db_owner**y haga clic en **Aceptar** para crear el usuario.  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>Para crear la instantánea de datos filtrados para la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en la publicación **AdvWorksSalesOrdersMerge** y, luego, haga clic en **Propiedades**.  
  
     Se mostrará el cuadro de diálogo **Propiedades de la publicación** .  
  
3.  Seleccione la página **Particiones de datos** y haga clic en **Agregar**.  
  
4.  En el **Agregar partición de datos** cuadro de diálogo, escriba `adventure-works\pamela0` en el **valor de HOST_NAME** cuadro y, a continuación, haga clic en **Aceptar**.  
  
5.  Seleccione la partición agregada recientemente, haga clic en **Generar instantáneas seleccionadas ahora**y, después, haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha creado correctamente una suscripción a la publicación de combinación y ha generado la instantánea filtrada para la nueva partición de datos de la suscripción, de manera que esté disponible cuando se inicialice la suscripción. A continuación, concederá derechos al Agente de mezcla en la base de datos de suscripciones y ejecutará el Agente de mezcla para iniciar la sincronización e inicializar la suscripción. Vea [Lección 3: Sincronizar la suscripción con la publicación de combinación](lesson-3-synchronizing-the-subscription-to-the-merge-publication.md).  
  
## <a name="see-also"></a>Vea también  
 [Subscribe to Publications](subscribe-to-publications.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Instantáneas para publicaciones de combinación con filtros con parámetros](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
