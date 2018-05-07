---
title: 'Tutorial: Configurar la replicación entre dos servidores conectados de forma continua (transaccional) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de374f4372f62741ff3c49a9433cf339cecf3d26
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>Tutorial: Configurar la replicación entre dos servidores conectados de forma continua (transaccional)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
La replicación transaccional es una buena solución para el problema de mover datos entre servidores conectados de forma continua. La utilización del Asistente para replicación, le facilitará la configuración y administración de una topología de replicación. Este tutorial le mostrará cómo configurar una topología de replicación transaccional para servidores conectados de forma continua. Para obtener más información sobre cómo funciona la replicación transaccional, vea [Introducción a la replicación transaccional](https://docs.microsoft.com/en-us/sql/relational-databases/replication/transactional/transactional-replication). 
  
## <a name="what-you-will-learn"></a>Aprendizaje  
Este tutorial le mostrará cómo publicar datos de una base de datos a otra con la replicación transaccional. 

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Crear un publicador mediante la replicación transaccional
> * Crear un suscriptor para el publicador transaccional
> * Validar la suscripción y medir la latencia
> * Metodología de solución de problemas de errores
  
  
## <a name="prerequisites"></a>Prerequisites  
Este tutorial está destinado a usuarios que están familiarizados con las operaciones básicas de las bases de datos, pero que tienen una experiencia limitada en operaciones de replicación. Para realizar este tutorial, es preciso que haya finalizado el anterior, [Preparar el servidor para replicación](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Para usar este tutorial, el sistema debe tener SQL Server Management Studio (SSMS) y los siguientes componentes:  
  
-   En el publicador (servidor de origen):  
  
    -   Cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto SQL Server Express o SQL Compact. Estas ediciones no pueden ser publicadores de replicación.   
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] Base de datos de ejemplo. Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada.  
  
-   En el suscriptor (servidor de destino):  
  
    -   Cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] no puede ser un suscriptor de replicación transaccional.  
  
- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Descargar una [Base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obtener instrucciones sobre cómo restaurar una base de datos en SSMS, vea [Restaurar una base de datos](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 
 
>[!NOTE]
> - La replicación no se admite entre SQL Server que estén separados por más de dos versiones entre sí. Para obtener más información, vea [Versiones de SQL admitidas en la topología de replicación](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], debe conectarse al publicador y al suscriptor con un inicio de sesión que sea miembro del rol fijo de servidor **sysadmin** . Para obtener más información sobre el rol sysadmin, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/sql/relational-databases/security/authentication-access/server-level-roles).  
  
  
**Tiempo estimado para completar este tutorial: 60 minutos.**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>Configurar el publicador para la replicación transaccional
En esta sección, creará una publicación transaccional con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para publicar un subconjunto filtrado de la tabla **Product** en la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. También agregará un inicio de sesión de SQL Server que utiliza el Agente de distribución para la lista de acceso a la publicación (PAL). Antes de iniciar este tutorial, deberá haber finalizado el tutorial anterior, [Preparar el servidor para replicación](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).


### <a name="create-a-publication-and-define-articles"></a>Crear publicaciones y definir artículos
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y luego expanda el nodo del servidor.  
  
2. Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Iniciar**. El Agente SQL Server debe estar ejecutándose antes de crear la publicación. Si esto no inicia el agente, deberá hacerlo manualmente desde el **Administrador de configuración de SQL Server**. 
3. Expanda la carpeta **Replicación**, haga clic con el botón derecho en la carpeta **Publicaciones locales** y, después, seleccione **Nueva publicación**.  Esto iniciará el Asistente para nueva publicación:  

    ![Nueva publicación](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. En la página Base de datos de publicaciones, seleccione [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]y, a continuación, seleccione **Siguiente**.  
  
4. En la página Tipo de publicación, seleccione **Publicación transaccional**y, a continuación, seleccione **Siguiente**:  

    ![replicación transaccional](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. En la página Artículos, expanda el nodo **Tablas**, seleccione la casilla **Producto**. A continuación, expanda **Producto** y desactive las casillas junto a **ListPrice** y **StandardCost**. Seleccione **Siguiente**:  

    ![Artículos para publicar](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. En la página Filtrar filas de tabla, seleccione **Agregar**.   
  
7. En el cuadro de diálogo **Agregar filtro**, seleccione la columna **SafetyStockLevel** y seleccione la flecha derecha para agregar la columna a la cláusula WHERE de la instrucción Filtrar en la consulta del filtro. Después, escriba manualmente en el modificador de la cláusula WHERE lo siguiente:  
  
    ```sql  
    WHERE [SafetyStockLevel] < 500  
    ```
  
    ![Instrucción de filtro](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. Seleccione **Aceptar**y luego seleccione **Siguiente**.  
  
9. Active la casilla **Crear una instantánea inmediatamente y mantenerla disponible para inicializar suscripciones** y seleccione **Siguiente**:  

    ![Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. En la página Seguridad del agente, desactive la casilla **Usar la configuración de seguridad del Agente de instantáneas** .   
  
    A. Seleccione **Configuración de seguridad** para el Agente de instantáneas, escriba <*Nombre_De_Equipo_Publicador>***\repl_snapshot** en el cuadro **Cuenta de proceso**, escriba la contraseña de la cuenta y, luego, seleccione **Aceptar**:  

    ![Seguridad del Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. Repita el paso anterior para establecer <*Nombre_De_Equipo_Publicador*>**\repl_logreader** como la cuenta de proceso para el Agente de registro del LOG y, después, seleccione **Aceptar**:  

    ![Seguridad del Agente de registro del LOG](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. En la página Finalización del asistente, escriba **AdvWorksProductTrans** en el cuadro **Nombre de publicación** y seleccione **Finalizar**:  

    ![Asignar nombre a la publicación](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. Una vez se haya creado la publicación, seleccione **Cerrar** para finalizar el asistente. 

    Puede producirse el siguiente error si no se está ejecutando el Agente SQL Server cuando intenta crear la publicación. Esto indica que la publicación se creó correctamente, pero no se pudo iniciar el Agente de instantáneas. Si esto ocurre, debe iniciar al Agente SQL Server y, después, iniciar manualmente el Agente de instantáneas. En la siguiente sección se indican las instrucciones para hacerlo: 

    ![No se puede iniciar el Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Para ver el estado de la generación de instantáneas  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales**, haga clic con el botón derecho en **AdvWorksProductTrans** y luego seleccione **Ver estado del Agente de instantáneas**:  

    ![Estado del Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3.  Se muestra el estado actual del trabajo del Agente de instantáneas para la publicación. Compruebe que el trabajo de instantáneas sea correcto antes de continuar con la siguiente sección.
          
    Si el Agente SQL Server no se estaba ejecutando cuando creó la publicación por primera vez, verá que el Agente de instantáneas "nunca se ejecutó" cuando comprueba el **estado del Agente de instantáneas** para su publicación. Si es así, seleccione **Iniciar** para iniciar el Agente de instantáneas: 

       ![Iniciar el Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
       Si ve un error aquí, consulte la sección [Solucionar problemas de errores con el Agente de instantáneas](#troubleshoot-erros-with-snapshot-agent). 

  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>Para agregar el inicio de sesión del Agente de distribución para la lista de acceso de la publicación (PAL)  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales**, haga clic con el botón derecho en **AdvWorksProductTrans** y luego seleccione **Propiedades**.  Se mostrará el cuadro de diálogo **Propiedades de la publicación** .    
  
    A. Seleccione la página **Lista de acceso a la publicación** y seleccione **Agregar**.  
    B. En el cuadro de diálogo **Agregar acceso de publicación**, seleccione <*Nombre_De_Equipo_Publicador>***\repl_distribution** y seleccione **Aceptar**. Seleccione **Aceptar**:

   
   ![Agregar el inicio de sesión a la lista PAL](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

**Vea también**:  
[Conceptos de la programación de replicación](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>Crear una suscripción a la publicación transaccional
En esta sección, agregará un suscriptor a la publicación que creada anteriormente. Este tutorial utiliza un suscriptor remoto (NODE2\SQL2016), pero también puede agregarse una suscripción localmente en el publicador. 

### <a name="to-create-the-subscription"></a>Para crear la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales**, haga clic con el botón derecho en la publicación **AdvWorksProductTrans** y, después, seleccione **Nuevas suscripciones**.  Se iniciará el Asistente para nueva suscripción: 
 
    ![Nueva suscripción](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3.  En la página Publicación, seleccione **AdvWorksProductTrans** y, a continuación, seleccione **Siguiente**:  

    ![Seleccione el publicador de transacciones](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4.  En la página Ubicación del Agente de distribución, seleccione **Ejecutar todos los agentes en el distribuidor** y luego seleccione **Siguiente**.  Para más información sobre las suscripciones de inserción y de extracción, vea [Suscribirse a publicaciones](https://docs.microsoft.com/en-us/sql/relational-databases/replication/subscribe-to-publications):

    ![Ejecutar Agentes de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5.  En la página Suscriptores, si no se muestra el nombre de la instancia del suscriptor, seleccione **Agregar suscriptor** y, después, seleccione **Agregar suscriptor de SQL Server** en la lista desplegable. Esto abrirá el cuadro de diálogo **Conectar al servidor**. Escriba el nombre de instancia del suscriptor y, después, seleccione **Conectar**.  
    
    A. Una vez que se haya agregado el suscriptor, active la casilla situada junto al nombre de instancia del suscriptor. Después, seleccione **Nueva base de datos** en **Base de datos de suscripción**:   

  ![Agregar servidor del suscriptor](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. Se abrirá el cuadro de diálogo **Nueva base de datos**. Escriba **ProductReplica** en el cuadro **Nombre de base de datos**, seleccione **Aceptar** y, después, seleccione **Siguiente**: 
  
    ![Base de datos de réplica de producto](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8.  En el cuadro de diálogo **Seguridad del Agente de distribución** seleccione el botón de puntos suspensivos (**...**). Escriba <*Nombre_De_Equipo_Publicador>***rpl_distribution** el cuadro **Cuenta de proceso**, escriba la contraseña para esta cuenta, seleccione **Aceptar** y, a continuación, **Siguiente**:

    ![Agregar una cuenta de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. Seleccione **Finalizar** para aceptar los valores predeterminados en las páginas restantes y finalizar el asistente.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Establecer permisos de base de datos en el suscriptor  
  
1.  Conéctese al suscriptor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión** y, después, seleccione **Nuevo inicio de sesión**.     
  
    A. En la página **General**, en **Nombre de inicio de sesión** seleccione **Buscar** y agregue el inicio de sesión para <*Nombre_De_Equipo>***\repl_distribution**.
    B. En la página **Asignaciones de usuario**, otorgue **db_owner** para la base de datos **ProductReplica**: 

    ![Iniciar sesión en el suscriptor](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Nuevo inicio de sesión**. 

  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Para ver el estado de sincronización de la suscripción  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor y luego la carpeta **Replicación** .  
  
2.  En la carpeta **Publicaciones locales**, expanda la publicación **AdvWorksProductTrans**, haga clic con el botón derecho en la suscripción de la base de datos **ProductReplica** y, después, seleccione **Ver estado de sincronización**. Se mostrará el actual estado de sincronización de la suscripción:  
    ![Ver estado de sincronización](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3.  Si la suscripción no está visible en **AdvWorksProductTrans**, presione F5 para actualizar la lista.  
  
**Vea también**:  
[Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Crear una suscripción de inserción](../../relational-databases/replication/create-a-push-subscription.md)  
[Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measuring-replication-latency"></a>Medir la latencia de replicación
En esta sección utilizará testigos de seguimiento para comprobar que los cambios se replican en el suscriptor y para determinar la latencia. La latencia es el tiempo necesario para que un cambio realizado en el publicador aparezca en el suscriptor.
  
1. Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor, haga clic con el botón derecho en la carpeta **Replicación** y luego seleccione **Iniciar el Monitor de replicación**:

    ![Iniciar el monitor de replicación](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. Expanda un grupo de publicador en el panel izquierdo, expanda una instancia de publicador y, a continuación, seleccione la publicación **AdvWorksProductTrans**.  
  
    A. Seleccione la pestaña **Testigos de seguimiento**.  
    B. Seleccione **Insertar seguimiento**.    
    c. Vea el tiempo transcurrido para el testigo de seguimiento en las siguientes columnas: **Publicador a distribuidor**, **Distribuidor a suscriptor**y **Latencia total**. El valor **Pendiente** indica que el testigo no ha alcanzado un punto específico:


   ![Testigo de seguimiento](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


**Vea también**   
[Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

## <a name="error-troubleshooting-methodology"></a>Metodología de solución de problemas de errores
Esta sección le explica cómo solucionar problemas de errores de sincronización de replicación básicos. Tenga en cuenta que esta sección está diseñada como una introducción para navegar por los componentes de replicación con el fin de solucionar los problemas. Pero los errores reales que se producen podrían ser diferentes de lo que se describe aquí y, por lo tanto, tendrán una resolución distinta. Si es así, es necesaria una solución de problemas adicional y está fuera del ámbito de este tutorial. 


### <a name="troubleshoot-errors-with-snapshot-agent"></a>Solucionar problemas de errores con el Agente de instantáneas
El **Agente de instantáneas** es el agente que genera la instantánea y la escribe en la carpeta de instantáneas especificada. 

1. Para ver el estado de su Agente de instantáneas, expanda el nodo **Publicación local** en la replicación, seleccione con el botón derecho su publicación **AdvWorksProductTrans** > **Ver estado del Agente de instantáneas**. 
2. Si se notifica un error en el **estado del Agente de instantáneas**, puede encontrar más detalles en el historial de trabajos del **Agente de instantáneas**. Para acceder a él, expanda **Agente SQL Server** en **Explorador de objetos** y abra el **Monitor de actividad de trabajo**. 

    A. Ordene por **Categoría** e identifique el **Agente de instantáneas** por la categoría "REPL Snapshot". 

    B. Haga clic con el botón derecho en el **Agente de instantáneas** y **Ver el historial**: 

   ![Historial del Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenthistory.png)
    
1. En el **Historial del Agente de instantáneas**, seleccione la entrada de registro correspondiente. Normalmente será una línea o dos *antes de* la entrada que informa del error (los errores se indican con una X roja).  Revise el texto del mensaje en el cuadro de texto situado debajo de los registros: 

    ![Acceso denegado del Agente de instantáneas](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotaccessdenied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.


  Si los permisos de ventanas no están configurados correctamente para la carpeta de instantáneas, verá un error de "acceso denegado" para el **Agente de instantáneas**. Debe comprobar los permisos para la cuenta de <*Nobre_De_Equipo_Publicador>***\repl_snapshot** en la carpeta repldata. Para obtener más información, vea [Crear un recurso compartido para la carpeta de instantáneas y asignar permisos](tutorial-preparing-the-server-for-replication.md#create-a-share-for-the-snapshot-folder-and-assign-permissions).

### <a name="troubleshoot-errors-with-log-reader-agent"></a>Solucionar problemas de errores con el Agente de registro del LOG
El **Agente de registro del LOG** se conecta a la base de datos del publicador y examina el registro de transacciones para las transacciones marcadas como "para replicación". Después, agrega las transacciones a la base de datos **Distribución**. 

1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor, haga clic con el botón derecho en la carpeta **Replicación** y luego seleccione **Iniciar el Monitor de replicación**:  

    ![Iniciar el monitor de replicación](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)
  
    Se inicial el monitor de replicación: ![Monitor de replicación](media/tutorial-replicating-data-between-continuously-connected-servers/replmonitor.png) 
   
2. La X roja es una indicación de que la publicación no se está sincronizando. Expanda **Mis publicadores** en el lado izquierdo y, después, expanda el servidor del publicador relevante.  
  
3.  Seleccione la publicación **AdvWorksProductTrans** de la izquierda y, después, busque la X roja en una de las pestañas para identificar dónde está el problema. En este caso, la X roja se encuentra en la **Pestaña Agentes**, que indica que uno de los agentes se ejecuta con un error: 

    ![Error de agente](media/tutorial-replicating-data-between-continuously-connected-servers/agenterror.png)

4. Seleccione la **Pestaña Agentes** para identificar el agente que tiene el error: 

    ![Error del registro del LOG](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentfailure.png)


5. Esta vista mostrará dos agentes, el **Agente de instantáneas** y el **Agente de registro del LOG**. El que tenga el error tendrá la X roja. En este caso, el **Agente de registro del LOG** es el que tiene la X roja, que indica que hay un problema con él. Haga doble clic en la línea en la que se informa del error, en este caso el **Agente de registro del LOG**. Se iniciará el **Historial del agente** del agente que haya seleccionado, en este caso el historial del **Agente de registro del LOG**. Esto proporciona información más detallada sobre el error: 
    
    ![Error del registro del LOG](media/tutorial-replicating-data-between-continuously-connected-servers/logreadererror.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. El error mencionado anteriormente se suele producir porque el propietario de la base de datos del publicador no está configurado correctamente. Esto suele suceder cuando se ha restaurado una base de datos. Para comprobarlo, expanda **Bases de datos** en **Explorador de objetos** > haga clic con el botón derecho en **AdventureWorks2012** > **Propiedades**. Compruebe la existencia de un propietario en la página **Archivos**. Si este campo está en blanco, esta es la causa probable del problema: 

    ![Propiedades de la base de datos](media/tutorial-replicating-data-between-continuously-connected-servers/dbproperties.png)

7. Si el propietario está en blanco en la página **Archivos**, abra una **Nueva ventana de consulta** dentro del contexto de la base de datos de **AdventureWorks2012**. Ejecute el siguiente fragmento de código de T-SQL:

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. Tendrá que reiniciar el **Agente de registro del LOG**. Para hacerlo, expanda el nodo **Agente SQL Server** en **Explorador de objetos** y abra el **Monitor de actividad de trabajo**. Ordene por **Categoría** e identifique el **Agente de registro del LOG** por la categoría **"REPL-LogReader"**. Haga clic con el botón derecho en el trabajo del **Agente de registro del LOG** y en **Iniciar trabajo en el paso**: 

    ![Reiniciar el Agente de registro del LOG](media/tutorial-replicating-data-between-continuously-connected-servers/startjobatstep.png)

9. Valide que la publicación se está sincronizando volviendo a abrir el **Monitor de replicación**. Si no está abierto, puede encontrarlo haciendo clic con el botón derecho en **Replicación** en **Explorador de objetos**. 
10. Seleccione la publicación **AdvWorksProductTrans**, luego la pestaña **Agentes** y haga doble clic en el **Agente de registro del LOG** para abrir el historial del agente. Ahora debería ver que el **Agente de registro del LOG** se está ejecutando y o bien está replicando comandos o que muestra "No hay transacciones replicadas":

    ![Registro del LOG en ejecución](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderrunning.png)

### <a name="troubleshoot-errors-with-distribution-agent"></a>Solucionar problemas de errores con el Agente de distribución
El **Agente de distribución** toma los datos que encuentra en la base de datos **Distribución** y, después, los aplica al suscriptor. 

1. Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el nodo del servidor, haga clic con el botón derecho en la carpeta **Replicación** y luego seleccione **Iniciar el Monitor de replicación**.  
2. En **Monitor de replicación**, seleccione la publicación **AdvWorksProductTrans** y seleccione la pestaña **Todas las suscripciones**. Haga clic con el botón derecho en la suscripción y, después, **Ver detalles**:

    ![Ver detalles de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/viewdetails.png)

2. Se abre el cuadro de diálogo de historial de **Distribuidor a suscriptor** y aclara qué tipo de error está detectando el agente: 

     ![Error de historial del Agente de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/disthistoryerror.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. El error indica que el **Agente de distribución** está volviendo a intentarlo. Para obtener más información, expanda **Agente SQL Server** en **Explorador de objetos** > **Monitor de actividad de trabajo**. Ordene los trabajos por **Categoría**. 

    A. Identifique el **Agente de distribución** por la categoría **"Distribución de replicación"**. Haga clic con el botón derecho en el agente y **Ver el historial**:

    ![Ver el historial del Agente de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/viewdistagenthistory.png)

5. Seleccione una de las entradas de error y vea el texto del error en la parte inferior de la ventana:  

    ![Contraseña incorrecta para el Agente de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/distpwwrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. Este error es una indicación de que la contraseña utilizada por el **Agente de distribución** es incorrecta. Para resolver este problema, expanda el nodo **Replicación** en **Explorador de objetos**, haga clic con el botón derecho en la suscripción > **Propiedades**. Seleccione el botón de puntos suspensivos (...) junto a **Cuenta de proceso del agente** y modifique la contraseña:

    ![Modificar la contraseña del agente de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/distagentpwchange.png)

7. Vuelva a comprobar el **Monitor de replicación**, que puede encontrar haciendo clic con el botón derecho en **Replicación** en **Explorador de objetos**. Una X roja debajo de **Todas las suscripciones** le indica que el **Agente de distribución** todavía detecta un error. Abra el historial de **Distribución al suscriptor** haciendo clic con el botón derecho en la suscripción en **Monitor de replicación** > **Ver detalles**. En este caso, el error ahora es diferente: 

    ![El agente de distribución no se puede conectar](media/tutorial-replicating-data-between-continuously-connected-servers/distagentcantconnect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. Este error indica que el **Agente de distribución** no se pudo conectar al suscriptor, ya que se produjo un error al iniciar sesión con el usuario **NODE2\repl_distribution**. Para investigar en profundidad, conéctese al suscriptor y abra el *actual* **registro de errores de SQL** en el nodo **Administración** en **Explorador de objetos**: 

    ![Error de inicio de sesión para el suscriptor](media/tutorial-replicating-data-between-continuously-connected-servers/loginfailed.png) Si ve este error, significa que falta el inicio de sesión en el suscriptor. Para solucionarlo, vea [Establecer permisos de base de datos en el suscriptor](#setting-database-permissions-at-the-subscriber).

9. Una vez resuelto el error de inicio de sesión, vuelva a comprobar el **Monitor de replicación**. Si se han abordado todos los problemas, debería ver una flecha verde junto al **nombre de la publicación** y un estado de **En ejecución** en **Todas las suscripciones**. Haga clic con el botón derecho en la **suscripción** para volver a iniciar el historial de **Distribuidor a suscriptor** para comprobar que se realizó correctamente. Si es la primera vez que se ejecuta el agente de distribución, verá que la instantánea ha sido copiada de forma masiva en el suscriptor como indica la figura siguiente: 

     ![Éxito del agente de distribución](media/tutorial-replicating-data-between-continuously-connected-servers/distagentsuccess.png)   

  ## <a name="next-steps"></a>Pasos siguientes
Ha configurado correctamente el publicador y el suscriptor para la replicación transaccional.  Ahora puede insertar, actualizar o eliminar datos en la tabla **Producto** del publicador. Después, puede consultar la tabla **Producto** en el suscriptor para ver los cambios replicados. El artículo siguiente le mostrará cómo configurar la replicación de mezcla.  

Vaya al siguiente artículo para obtener más información
> [!div class="nextstepaction"]
> [Pasos siguientes](tutorial-replicating-data-with-mobile-clients.md)

  
