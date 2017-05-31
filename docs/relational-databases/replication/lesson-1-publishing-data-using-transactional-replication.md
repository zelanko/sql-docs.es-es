---
title: "Lección 1: Publicación de datos con la replicación transaccional | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 021ff6838de18ea03a50aae661d543061088ae87
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>Lección 1: Publicar datos con la replicación transaccional
En esta lección, creará una publicación transaccional con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar un subconjunto filtrado de la tabla **Product** en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . También agregará un inicio de sesión de SQL Server que utiliza el Agente de distribución para la lista de acceso a la publicación (PAL). Antes de iniciar este tutorial, deberá haber finalizado el tutorial anterior, [Preparar el servidor para replicación](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
### <a name="to-create-a-publication-and-define-articles"></a>Para crear publicaciones y definir artículos  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** , haga clic con el botón derecho en la carpeta **Publicaciones locales** y, después, haga clic en **Nueva publicación**.  
  
    Se iniciará el Asistente para nueva publicación.  
  
3.  En la página Base de datos de publicaciones, seleccione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]y, a continuación, haga clic en **Siguiente**.  
  
4.  En la página Tipo de publicación, seleccione **Publicación transaccional**y, a continuación, haga clic en **Siguiente**.  
  
5.  En la página Artículos, expanda el nodo **Tablas** , active la casilla **Product** , expanda **Product** y, a continuación, desactive las casillas **ListPrice** y **StandardCost** . Haga clic en **Siguiente**.  
  
6.  En la página Filtrar filas de tabla, haga clic en **Agregar**.  
  
7.  En el cuadro de diálogo **Agregar filtro** , haga clic en la columna **SafetyStockLevel** , haga clic en la flecha derecha para agregar la columna a la cláusula WHERE de la instrucción Filtrar en la consulta del filtro y modifique la cláusula WHERE de la manera siguiente:  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  Haga clic en **Aceptar**y, a continuación, en **Siguiente**.  
  
9. Active la casilla **Crear una instantánea inmediatamente y mantenerla disponible para inicializar suscripciones** y haga clic en **Siguiente**.  
  
10. En la página Seguridad del agente, desactive la casilla **Usar la configuración de seguridad del Agente de instantáneas** .  
  
11. Haga clic en **Configuración de seguridad** para el Agente de instantáneas, escriba \<*nombreDeEquipo>***\repl_snapshot** en el cuadro **Cuenta de proceso**, escriba la contraseña de la cuenta y luego haga clic en **Aceptar**.  
  
12. Repita el paso anterior para establecer repl_logreader como la cuenta de proceso para el Agente de registro del LOG y, después, haga clic en **Finalizar**.  
  
13. En la página Finalización del asistente, escriba **AdvWorksProductTrans** en el cuadro **Nombre de publicación** y haga clic en **Finalizar**.  
  
14. Una vez se haya creado la publicación, haga clic en **Cerrar** para finalizar el asistente.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Para ver el estado de la generación de instantáneas  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en **AdvWorksProductTrans**y luego en **Ver estado del Agente de instantáneas**.  
  
3.  Se muestra el estado actual del trabajo del Agente de instantáneas para la publicación. Compruebe que el trabajo de instantáneas sea correcto antes de continuar con la siguiente lección.  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>Para agregar el inicio de sesión del Agente de distribución para la lista de acceso de la publicación (PAL)  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales** , haga clic con el botón derecho en **AdvWorksProductTrans**y luego en **Propiedades**.  
  
    Se mostrará el cuadro de diálogo **Propiedades de la publicación** .  
  
3.  Seleccione la página **Lista de acceso a la publicación** y haga clic en **Agregar**.  
  
4.  \En el cuadro de diálogo **Agregar acceso de publicación**, seleccione *<nombre_equipo>***\repl_distribution** y haga clic en **Aceptar**. Haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
Ha creado correctamente la publicación transaccional. A continuación se suscribirá a esta publicación. Consulte [Lección 2: Crear una suscripción a la publicación transaccional](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
## <a name="see-also"></a>Vea también  
[Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)  
[Definir un artículo](../../relational-databases/replication/publish/define-an-article.md)  
[Crear y aplicar una instantánea](../../relational-databases/replication/create-and-apply-the-snapshot.md)  
  
  
  

