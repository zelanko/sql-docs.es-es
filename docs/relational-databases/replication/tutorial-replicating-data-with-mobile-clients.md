---
title: 'Tutorial: Configurar la replicación entre un servidor y clientes móviles (de mezcla) | Microsoft Docs'
ms.custom: ''
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d9751b7adc3d2cd4169bcd6b3a174de720c05eb9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>Tutorial: Configurar la replicación entre un servidor y clientes móviles (de mezcla)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
La replicación de mezcla es una buena solución al problema de mover datos entre un servidor central y clientes móviles que solo se conectan en determinadas ocasiones. La utilización de asistentes para replicación le facilitará la configuración y administración de una topología de replicación de mezcla. Este tutorial le mostrará cómo configurar una topología de replicación para clientes móviles.  Para obtener más información sobre la replicación de mezcla, vea [Visión general de la replicación de mezcla](https://docs.microsoft.com/en-us/sql/relational-databases/replication/merge/merge-replication)
  
## <a name="what-you-will-learn"></a>Aprendizaje  
Este tutorial le enseña cómo usar la replicación de mezcla para publicar datos de una base de datos central en uno o más usuarios móviles para que cada usuario obtenga un subconjunto de datos filtrado de manera exclusiva. 

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Configurar un publicador para la replicación de mezcla
> * Agregar un suscriptor móvil para la publicación de mezcla
> * Sincronizar la suscripción con la publicación de combinación
  
## <a name="prerequisites"></a>Prerequisites  
Este tutorial está destinado a usuarios que están familiarizados con las operaciones básicas de las bases de datos, pero que tienen una experiencia limitada en operaciones de replicación. Antes de comenzar este tutorial, debe completar el [Tutorial: Preparar el servidor para la replicación](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para utilizar este tutorial, el sistema debe tener instalado SQL Server Management Studio los siguientes componentes:  
  
-   En el publicador (servidor de origen):  
  
    -   Cualquier edición de SQL Server, excepto SQL Server Express o SQL Server Compact. Estas ediciones no pueden ser publicadores de replicación.   
    -   La base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada.  
  
-   En el suscriptor (servidor de destino):  
  
    -   Cualquier edición de SQL Server, excepto para [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] no es compatible con la publicación creada en este tutorial. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Descargar una [Base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obtener instrucciones sobre cómo restaurar una base de datos en SSMS, vea [Restaurar una base de datos](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  
 
  
>[!NOTE]
> - La replicación no se admite entre SQL Server que estén separados por más de dos versiones entre sí. Para obtener más información, vea [Versiones de SQL admitidas en la topología de replicación](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], debe conectarse al publicador y al suscriptor con un inicio de sesión que sea miembro del rol fijo de servidor **sysadmin** . Para obtener más información sobre el rol sysadmin, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Tiempo estimado para completar este tutorial: 60 minutos.**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>Configurar un publicador para la replicación de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
En esta sección, creará una publicación de combinación con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar un subconjunto de las tablas **Employee**, **SalesOrderHeader** y **SalesOrderDetail** en la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. Estas tablas están filtradas con filtros de fila con parámetros para que cada suscripción contenga una partición única de los datos. También agregará el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa el Agente de mezcla a la lista de acceso a la publicación (PAL).  
  
### <a name="create-merge-publication-and-define-articles"></a>Crear publicaciones de mezcla y definir artículos  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2. Inicie el **Agente SQL Server** haciendo clic con el botón derecho en **Explorador de objetos** y seleccionando **Iniciar**. Si esto no inicia el agente, deberá hacerlo manualmente desde el **Administrador de configuración de SQL Server**.  
3. Expanda la carpeta **Replicación**, haga clic con el botón derecho en la carpeta **Publicaciones locales**y, después, seleccione **Nueva publicación**.  Se iniciará el Asistente para nueva publicación:  

    ![Inicie el Asistente para nueva publicación](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3.  En la página Base de datos de publicaciones, seleccione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]y, a continuación, seleccione **Siguiente**. 

      
4.  En la página Tipo de publicación, seleccione **Publicación de combinación**y, a continuación, seleccione **Siguiente**.  
    A. En la página Tipos de suscriptor, asegúrese de que solo esté seleccionado [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior y, a continuación, seleccione **Siguiente**: 

    ![Replicación de mezcla](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6.  En la página Artículos, expanda el nodo **Tablas** y seleccione las siguientes tres tablas: **Employee**, **SalesOrderHeader** y **SalesOrderDetail**. Seleccione **Siguiente**:  

    ![Artículos de mezcla](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

    >[!NOTE]
    > La tabla Employee contiene una columna (OrganizationNode) que tiene el tipo de datos hierarchyid, que solo se admite para la replicación en SQL 2017. Si usa una versión anterior a SQL 2017, verá un mensaje en la parte inferior de la pantalla que le notifica de posibles pérdidas de datos si usa esta columna en la replicación bidireccional. Para los fines de este tutorial, puede hacer caso omiso de este mensaje. Pero este tipo de datos no debería replicarse en un entorno de producción a menos que esté usando la versión compatible. Para obtener más información sobre cómo replicar el tipo de datos hierarchyid, vea [Usar columnas Hierarchyid en la replicación](https://docs.microsoft.com/en-us/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)
    
  
7.  En la página Filtrar filas de tabla, seleccione **Agregar** y luego **Agregar filtro**.  
  
8.  En el cuadro de diálogo **Agregar filtro**, seleccione **Employee (HumanResources)** en **Seleccione la tabla que desea filtrar**. Seleccione la columna **LoginID**, seleccione la flecha derecha para agregar la columna a la cláusula WHERE de la consulta del filtro y modifique la cláusula WHERE de la manera siguiente:  
  
    ```sql 
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
    A. Seleccione **Una fila de esta tabla irá a una sola suscripción**y luego **Aceptar**:  
 
    ![Agregar filtro](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. En la página **Filtrar filas de tabla**, seleccione **Employee (Human Resources)**, luego **Agregar** y, después, **Agregar combinación para ampliar el filtro seleccionado**.  
  
    A. En el cuadro de diálogo **Agregar combinación**, seleccione **Sales.SalesOrderHeader** en **Tabla combinada**. Seleccione **Escribir instrucción de combinación manualmente** y complete la instrucción de combinación de la manera siguiente:  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    B. En **Especifique las opciones de combinación**, seleccione **Clave única**y, a continuación, seleccione **Aceptar**:

    ![Agregar combinación para filtrar](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. En la página Filtrar filas de tabla, seleccione **SalesOrderHeader**, luego **Agregar** y, después, **Agregar combinación para ampliar el filtro seleccionado**.  
  
    A. En el cuadro de diálogo **Agregar combinación** , seleccione **Sales.SalesOrderDetail** en **Tabla combinada**.    
    B. Seleccione **Usar generador de instrucciones para crear la instrucción**.  
    c. En el cuadro **Vista previa**, confirme que la instrucción de combinación es como sigue:  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. En **Especifique las opciones de combinación**, seleccione **Clave única**y, a continuación, seleccione **Aceptar**. Seleccione **Siguiente**: 

       ![Combinar tablas de pedido de ventas](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. Seleccione **Crear una instantánea inmediatamente**, desactive **Programar el Agente de instantáneas para ejecutarse**y, a continuación, seleccione **Siguiente**:  

    ![Crear una instantánea inmediatamente](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. En la página Seguridad del agente, seleccione **Configuración de seguridad**, escriba <*Nombre_De_Equipo_Publicador>***\repl_snapshot** en el cuadro **Cuenta de proceso**, escriba la contraseña de la cuenta y seleccione **Aceptar**. Seleccione **Siguiente**:  

    ![Seguridad del Agente de instantáneas](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. En la página **Finalización del asistente**, escriba **AdvWorksSalesOrdersMerge** en el cuadro **Nombre de publicación** y seleccione **Finalizar**:  

    ![Asignar nombre a la replicación de mezcla](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. Una vez creada la publicación, seleccione **Cerrar**. En el nodo **Replicación** en **Explorador de objetos**, haga clic con el botón derecho en **Publicaciones locales** y en **Actualizar** para ver la nueva replicación de mezcla.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Para ver el estado de la generación de instantáneas  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta Publicaciones locales, haga clic con el botón derecho en **AdvWorksSalesOrdersMerge**y luego seleccione **Ver estado del Agente de instantáneas**:  

    ![Ver estado del Agente de instantáneas](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3.  Se muestra el estado actual del trabajo del Agente de instantáneas para la publicación. Compruebe que el trabajo de instantáneas sea correcto antes de continuar con la siguiente lección.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>Para agregar el inicio de sesión del Agente de mezcla para la lista de acceso de la publicación (PAL)  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta Publicaciones locales, haga clic con el botón derecho en **AdvWorksSalesOrdersMerge**y luego seleccione **Propiedades**.  
  
    A. Seleccione la página **Lista de acceso a la publicación** y seleccione **Agregar**. 
  
    B. En el cuadro de diálogo Agregar acceso de publicación, seleccione *<Nombre_De_Equipo_Publicador>***\repl_merge** y seleccione **Aceptar**. Seleccione **Aceptar**: 

    ![Combinar PAL](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
**Vea también**:  
[Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)  
[Filtros de fila con parámetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
[Definir un artículo](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="creating-a-subscription-to-the-merge-publication"></a>Crear una suscripción a la publicación de combinación
En esta sección, agregará una suscripción a la publicación de mezcla que creó anteriormente. Este tutorial usa el suscriptor remoto (NODE2\SQL2016). Luego establecerá los permisos en la base de datos de suscripciones y generará manualmente la instantánea de datos filtrados para la nueva suscripción.   
  
### <a name="add-a-subscriber-for-merge-publication"></a>Agregar un suscriptor para la publicación de mezcla
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y expanda el nodo de servidor. Expanda la carpeta **Replicación**, haga clic con el botón derecho en la carpeta **Suscripciones locales** y luego seleccione **Nuevas suscripciones**. Se iniciará el Asistente para nueva suscripción:

    ![Nueva suscripción](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2.  En la página **Publicación**, seleccione **Buscar publicador de SQL Server** en la lista **Publicador**.  
  
    A. En el cuadro de diálogo **Conectar al servidor**, escriba el nombre de la instancia del publicador en el cuadro **Nombre del servidor** y, después, seleccione **Conectar**: 

    ![Agregar publicador en la publicación](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4.  Seleccione **AdvWorksSalesOrdersMerge** y **Siguiente**.  
  
5.  En la página Ubicación del Agente de mezcla, seleccione **Ejecutar cada agente en su suscriptor**y, luego, **Siguiente**:  

    ![Suscripción de extracción](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6.  En la página Suscriptores, seleccione el nombre de instancia del servidor del suscriptor y, en **Base de datos de suscripciones**, seleccione **Nueva base de datos** de la lista.  
  
    A. En el cuadro de diálogo **Nueva base de datos**, escriba **SalesOrdersReplica** en el cuadro **Nombre de la base de datos**, seleccione **Aceptar** y, después, **Siguiente**: 

    ![Agregar base de datos a Sub](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8.  En la página Seguridad del Agente de mezcla, seleccione el botón de puntos suspensivos (**…**), escriba <*Nombre_De_Equipo_Suscriptor>***\repl_merge* en el cuadro **Cuenta de proceso**, escriba la contraseña de esta cuenta, seleccione **Aceptar**, luego **Siguiente** y, después, otra vez **Siguiente**:  

    ![Seguridad del Agente de mezcla](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. En la **Programación de sincronización**, establezca **Programación del agente** en **Ejecutar solamente a petición**. Seleccione **Siguiente**:  

    ![Programación de sincronización](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. En la página Inicializar suscripciones, seleccione **En la primera sincronización** de la lista **Inicializar cuando**, seleccione **Siguiente** y, después, otra vez **Siguiente**: 

    ![Primera sincronización](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. En la página Valores de HOST_NAME, escriba un valor para **adventure-works\pamela0** en el cuadro **Valor de HOST_NAME** y, después, seleccione **Finalizar**:  

    ![Hostname](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. Vuelva a seleccionar **Finalizar** y, una vez creada la suscripción, seleccione **Cerrar**.  

### <a name="setting-server-permissions-at-the-subscriber"></a>Establecer permisos de servidor en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión** y, después, seleccione **Nuevo inicio de sesión**.  
  
    A. En la página **General**, seleccione **Buscar**, escriba <*Nombre_De_Equipo_Suscriptor>***\repl_merge** en el campo **Escriba el nombre de objeto**, seleccione **Comprobar nombres** y **Aceptar**: 
    
    ![Iniciar sesión en el suscriptor](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. En la página **Asignación de usuario**, seleccione la base de datos **SalesOrdersReplica** y seleccione el rol **db_owner**.  En la página **Elementos protegibles**, conceda el permiso "Explícito" para **Modificar seguimiento**. Seleccione **Aceptar**:

    ![Establecer el inicio de sesión como DBO en Sub](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>Para crear la instantánea de datos filtrados para la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales**, haga clic con el botón derecho en la publicación **AdvWorksSalesOrdersMerge** y, luego, seleccione **Propiedades**.  
   
    A. Seleccione la página **Particiones de datos** y seleccione **Agregar**.   
    B. En el cuadro de diálogo **Agregar partición de datos**, escriba **adventure-works\pamela0** en el cuadro **Valor de HOST_NAME** y, después, seleccione **Aceptar**.  
    c. Seleccione la partición agregada recientemente, seleccione **Generar instantáneas seleccionadas ahora** y, después, seleccione **Aceptar**: 

    ![Agregar partición](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
**Vea también**:  
[Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
[Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)  
[Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>Sincronizar la suscripción con la publicación de combinación

En esta sección iniciará el Agente de mezcla para inicializar la suscripción con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. También utilizará este procedimiento para sincronizar con el publicador.   
  
### <a name="to-start-synchronization-and-initialize-the-subscription"></a>Para iniciar la sincronización e inicializar la suscripción  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
2. Asegúrese de que el **Agente SQL Server** se está ejecutando. Si no lo está, haga clic con el botón derecho en el **Agente SQL Server** en **Explorador de objetos** y seleccione **Iniciar**. Si esto no inicia el agente, deberá hacerlo manualmente mediante el **Administrador de configuración de SQL Server**. 
  
2.  Expanda el nodo **Replicación**. En la carpeta **Suscripciones locales**, haga clic con el botón derecho en la suscripción de la base de datos **SalesOrdersReplica** y, después, seleccione **Ver estado de sincronización**.  
  
    A. Seleccione **Inicio** para inicializar la suscripción: 

    ![Estado de sincronización](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
### <a name="next-steps"></a>Next Steps  
Ha configurado correctamente el publicador y el suscriptor para la replicación de mezcla.  También puede insertar, actualizar o eliminar datos en las tablas **SalesOrderHeader** o **SalesOrderDetail** en el publicador o en el suscriptor, repetir este procedimiento cuando exista conectividad de red para sincronizar datos entre el publicador y el suscriptor y, después, consultar las tablas **SalesOrderHeader** o **SalesOrderDetail** en el otro servidor para ver los cambios replicados.  
  
**Vea también**:   
[Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Sincronizar datos](../../relational-databases/replication/synchronize-data.md)  
[Sincronizar una suscripción de extracción](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
