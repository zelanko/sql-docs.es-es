---
title: "Crear una instant&#225;nea para una publicaci&#243;n de mezcla con filtros con par&#225;metros | Microsoft Docs"
ms.custom: ""
ms.date: "05/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "filtros con parámetros [replicación de SQL Server], instantáneas"
  - "instantáneas [replicación de SQL Server], filtros con parámetros e"
  - "filtros [replicación de SQL Server], con parámetros"
ms.assetid: 00dfb229-f1de-4d33-90b0-d7c99ab52dcb
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Crear una instant&#225;nea para una publicaci&#243;n de mezcla con filtros con par&#225;metros
  En este tema se describe cómo se crea una instantánea de una publicación de combinación con filtros con parámetros en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para crear una instantánea de una publicación de combinación con filtros con parámetros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si desea generar una instantánea de una publicación de combinación mediante filtros con parámetros, debe generar primero una instantánea estándar (o de esquema) que contenga todos los datos publicados y los metadatos del Suscriptor para la suscripción. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md). Después de haber creado la instantánea del esquema, puede generar la instantánea que contiene la partición específica del Suscriptor de los datos publicados.  
  
-   Si el filtrado de uno o más artículos de la publicación produce particiones no superpuestas y únicas para cada suscripción, los metadatos se limpian cada vez que se ejecuta el Agente de mezcla. Esto significa que la instantánea con particiones expira antes. Cuando utilice esta opción, puede ser conveniente permitir a los suscriptores que inicien la generación y entrega de instantáneas. Para obtener más información acerca de opciones de filtrado, consulte la sección "Configurar la partición del opciones" de [instantáneas para publicaciones de mezcla con filtros parametrizados](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Generar instantáneas para las particiones en el **particiones de datos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Puede permitir a los suscriptores iniciar la generación y entrega de instantáneas y/o generar instantáneas.  
  
 Antes de generar instantáneas de una o varias particiones debe:  
  
1.  Crear una publicación de combinación con el Asistente para nueva publicación y especificar uno o varios filtros de fila con parámetros en la página **Agregar filtro** del asistente. Para más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
2.  Generar una instantánea del esquema para la publicación. De forma predeterminada, se genera una instantánea del esquema al completar el Asistente para nueva publicación, aunque también puede generar una instantánea del esquema desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### Para generar una instantánea del esquema  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, la carpeta **Publicaciones** .  
  
3.  Haga clic en la publicación para la que desea crear una instantánea y, a continuación, haga clic en **Ver estado del agente de instantáneas**.  
  
4.  En el **Ver estado del agente de instantáneas - \< publicación>** cuadro de diálogo, haga clic en **iniciar**.  
  
     Cuando el Agente de instantáneas termina de generar la instantánea, aparece un mensaje del tipo "[100%] Se ha generado una instantánea de 17 artículos".  
  
#### Para permitir a los suscriptores inicializar la generación y distribución de instantáneas  
  
1.  En el **particiones de datos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione **definir una partición y generar una instantánea si es necesario cuando un suscriptor nuevo intente sincronizar automáticamente**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### Para generar y actualizar instantáneas  
  
1.  En el **particiones de datos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Agregar**.  
  
2.  Escriba un valor para el **HOST_NAME ()** o **SUSER_SNAME ()** valor asociado a la partición que desea crear una instantánea.  
  
3.  También puede especificar una programación para actualizar las instantáneas:  
  
    1.  Seleccione **programar el agente de instantáneas para esta partición para que se ejecute a las horas siguientes**  
  
    2.  Acepte la programación predeterminada para actualizar instantáneas o haga clic en **Cambiar** para especificar una programación diferente.  
  
4.  Haga clic en **Aceptar**, que le devuelve el **Propiedades de la publicación - \< publicación>** cuadro de diálogo.  
  
5.  Seleccione la partición en la cuadrícula de propiedades y, a continuación, haga clic en **Generar instantáneas seleccionadas ahora**.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Con los procedimientos almacenados y el Agente de instantáneas, podrá hacer lo siguiente:  
  
-   Permita a los suscriptores que soliciten la generación y aplicación de instantáneas la primera vez que se sincronicen.  
  
-   Genere previamente las instantáneas para cada partición.  
  
-   Generar manualmente una instantánea para cada Suscriptor.  
  
    > [!IMPORTANT]  
    >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
#### Para crear una publicación que permita a los suscriptores iniciar la generación y entrega de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique los parámetros siguientes:  
  
    -   El nombre de la base de datos de publicación para **@publication**.  
  
    -   Un valor de **es true** de **@allow_subscriber_initiated_snapshot**, lo que permite a los suscriptores iniciar el proceso de instantáneas.  
  
    -   (Opcional) El número de procesos de instantáneas dinámicas que se pueden ejecutar simultáneamente para **@max_concurrent_dynamic_snapshots**. Si se está ejecutando el número máximo de procesos y un Suscriptor intenta generar una instantánea, el proceso se coloca en una cola. De forma predeterminada, no hay límite al número de procesos simultáneos.  
  
2.  En el publicador, ejecute [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especificar el nombre de publicación utilizado en el paso 1 para **@publication** y la [!INCLUDE[msCoName](../../includes/msconame-md.md)] las credenciales de Windows en la que la [agente de instantáneas de replicación](../../relational-databases/replication/agents/replication-snapshot-agent.md) se ejecuta para **@job_login** y **@password**. Si va a utilizar el agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectar con el publicador, también debe especificar un valor de **0** de **@publisher_security_mode** y el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación. Para obtener más información sobre cómo generar una instantánea inicial y definir una programación personalizada para el Agente de instantáneas, vea [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores proporcionados para todos los parámetros, incluidos *valor de job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Ejecutar [sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para agregar artículos a la publicación. Este procedimiento almacenado se debe ejecutar una vez para cada artículo de la publicación. Cuando se utiliza filtros parametrizados, debe especificar un filtro de fila parametrizado para uno o más artículos con el **@subset_filterclause** parámetro. Para más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Si otros artículos se filtrarán basándose en el filtro de fila parametrizado, ejecutar [sp_addmergefilter & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir la unión o relaciones de registros lógicos entre los artículos. Este procedimiento almacenado se debe ejecutar una vez para cada relación que se está definiendo. Para más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Cuando el Agente de mezcla solicita a la instantánea que inicialice el Suscriptor, se genera automáticamente la instantánea para la partición de la suscripción solicitante.  
  
#### Para crear una publicación y pregenerar o actualizar automáticamente las instantáneas  
  
1.  Ejecutar [sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) Para crear la publicación. Para obtener más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  En el publicador, ejecute [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especificar el nombre de publicación utilizado en el paso 1 para **@publication** y las credenciales de Windows en la que se ejecuta el agente de instantáneas para **@job_login** y **@password**. Si va a utilizar el agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectar con el publicador, también debe especificar un valor de **0** de **@publisher_security_mode** y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación. Para obtener más información sobre cómo generar una instantánea inicial y definir una programación personalizada para el Agente de instantáneas, vea [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores proporcionados para todos los parámetros, incluidos *valor de job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Ejecutar [sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para agregar artículos a la publicación. Este procedimiento almacenado se debe ejecutar una vez para cada artículo de la publicación. Cuando se utiliza filtros parametrizados, debe especificar un filtro de fila con parámetros para un artículo utilizando el **@subset_filterclause** parámetro. Para más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Si otros artículos se filtrarán basándose en el filtro de fila parametrizado, ejecutar [sp_addmergefilter & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir la unión o relaciones de registros lógicos entre los artículos. Este procedimiento almacenado se debe ejecutar una vez para cada relación que se está definiendo. Para obtener más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especifica el valor de **@publication** desde el paso 1. Tenga en cuenta el valor de la **snapshot_jobid** en el resultado de establecer.  
  
6.  Convertir el valor de la **snapshot_jobid** obtenido en el paso 5 para **uniqueidentifier**.  
  
7.  En el publicador de la **msdb** base de datos, ejecutar [sp_start_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), especificando el valor convertido obtenido en el paso 6 para **@job_id**.  
  
8.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepartition & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md). Especifique el nombre de la publicación desde el paso 1 para **@publication** y el valor que se utiliza para definir la partición para **@suser_sname** Si [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) se utiliza en la cláusula de filtro o para **@host_name** Si [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) se utiliza en la cláusula de filtro.  
  
9. En el publicador de la base de datos de publicación, ejecute [sp_adddynamicsnapshot_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md). Especifique el nombre de la publicación desde el paso 1 para **@publication**, el valor de **@suser_sname** o **@host_name** desde el paso 8 y una programación para el trabajo. Esto crea el trabajo que genera la instantánea con parámetros para la partición especificada. Para más información, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!NOTE]  
    >  Este trabajo se ejecuta usando la misma cuenta de Windows que el trabajo de la instantánea inicial definido en el paso 2. Para quitar el trabajo de instantáneas con parámetros y su partición de datos relacionados, ejecutar [sp_dropdynamicsnapshot_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md).  
  
10. En el publicador de la base de datos de publicación, ejecute [sp_helpmergepartition & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md), especifica el valor de **@publication** desde el paso 1 y el valor de **@suser_sname** o **@host_name** desde el paso 8. Tenga en cuenta el valor de la **dynamic_snapshot_jobid** en el resultado de establecer.  
  
11. En el distribuidor de la **msdb** base de datos, ejecutar [sp_start_job & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md), especificando el valor obtenido en el paso 9 para **@job_id**. Esto inicia el trabajo de instantánea con parámetros para la partición.  
  
12. Repita los pasos 8-11 para generar una instantánea con particiones para cada suscripción.  
  
#### Para crear una publicación y crear manualmente instantáneas para cada partición  
  
1.  Ejecutar [sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) Para crear la publicación. Para obtener más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  En el publicador, ejecute [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especificar el nombre de publicación utilizado en el paso 1 para **@publication** y las credenciales de Windows en la que se ejecuta el agente de instantáneas para **@job_login** y **@password**. Si va a utilizar el agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación al conectar con el publicador, también debe especificar un valor de **0** de **@publisher_security_mode** y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información de inicio de sesión de **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación. Para obtener más información sobre cómo generar una instantánea inicial y definir una programación personalizada para el Agente de instantáneas, vea [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores proporcionados para todos los parámetros, incluidos *valor de job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
3.  Ejecutar [sp_addmergearticle & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) Para agregar artículos a la publicación. Este procedimiento almacenado se debe ejecutar una vez para cada artículo de la publicación. Cuando se utiliza filtros parametrizados, debe especificar un filtro de fila parametrizado para al menos un artículo utilizando el **@subset_filterclause** parámetro. Para más información, consulte [Define and Modify a Parameterized Row Filter for a Merge Article](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
4.  Si otros artículos se filtrarán basándose en el filtro de fila parametrizado, ejecutar [sp_addmergefilter & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir la unión o relaciones de registros lógicos entre los artículos. Este procedimiento almacenado se debe ejecutar una vez para cada relación que se está definiendo. Para más información, consulte [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
5.  Inicie el trabajo de la instantánea o ejecute el Agente de instantáneas de replicación desde el símbolo del sistema para generar el esquema de instantáneas estándar y otros archivos. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
6.  Vuelva a ejecutar el agente de instantáneas de replicación desde la línea de comandos para generar archivos de bulk copy (bcp), especifica la ubicación de la instantánea con particiones para **- DynamicSnapshotLocation** y una o ambas de las siguientes propiedades que define la partición:  
  
    -   **DynamicFilterHostName -** -el valor si [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) se utiliza.  
  
    -   **-DynamicFilterLogin** -el valor si [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md) se utiliza.  
  
7.  Repita el paso 6 para generar una instantánea con particiones para cada suscripción.  
  
8.  Ejecute el Agente de mezcla para que cada suscripción aplique la instantánea con particiones inicial en los Suscriptores, especificando las propiedades siguientes:  
  
    -   **-Hostname** -el valor utilizado para definir la partición si se invalida el valor real de HOST_NAME.  
  
    -   **-DynamicSnapshotLocation** -la ubicación de la instantánea dinámica para esta partición.  
  
> [!NOTE]  
>  Para obtener más información sobre la programación de los agentes de replicación, vea [conceptos de los ejecutables del agente de replicación](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este ejemplo crea una publicación de combinación con filtros con parámetros donde los Suscriptores inician el proceso de generación de instantáneas. Los valores para **@job_login** y **@job_password** se pasan en el uso de variables de secuencias de comandos.  
  
 [!code-sql[HowTo#sp_MergeDynamicPub1](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_1.sql)]  
  
 Este ejemplo crea una publicación con un filtro parametrizado donde cada suscriptor tiene su partición definida ejecutando [sp_addmergepartition](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md) y el trabajo de instantánea filtrado creado ejecutando [sp_adddynamicsnapshot_job](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md) pasar la información de partición. Los valores para **@job_login** y **@job_password** se pasan en el uso de variables de secuencias de comandos.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_2.sql)]  
  
 Este ejemplo crea una publicación mediante un filtro con parámetros donde cada Suscriptor debe tener su partición de datos y el trabajo de instantánea filtrado creado proporcionando la información de la partición. Un Suscriptor proporciona información de la partición mediante los parámetros de línea de comandos al ejecutar manualmente los agentes de replicación. Este ejemplo supone que también se ha creado una suscripción a la publicación.  
  
 [!code-sql[HowTo#sp_MergeDynamicPubPartitionManual](../../relational-databases/replication/codesnippet/tsql/create-a-snapshot-for-a-_3.sql)]  
  
```  
  
REM Line breaks are added to improve readability.   
REM In a batch file, commands must be made in a single line.  
REM Run the Snapshot agent from the command line to generate the standard snapshot   
REM schema and other files.   
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub% -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  
  
PAUSE  
  
```  
  
```  
  
REM Run the Snapshot agent from the command line, this time to generate   
REM the bulk copy (.bcp) data for each Subscriber partition.    
SET DistPub=%computername%  
SET PubDB=AdventureWorks2012   
SET PubName=AdvWorksSalesPersonMerge  
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
MD %SnapshotDir%  
  
"C:\Program Files\Microsoft SQL Server\120\COM\SNAPSHOT.EXE" -Publication %PubName%    
-Publisher %DistPub%  -Distributor  %DistPub%  -PublisherDB %PubDB%  -ReplicationType 2    
-OutputVerboseLevel 1  -DistributorSecurityMode 1  -DynamicFilterHostName "adventure-works\Fernando"    
-DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
```  
  
REM Run the Merge Agent for each subscription to apply the partitioned   
REM snapshot for each Subscriber.    
SET Publisher = %computername%  
SET Subscriber = %computername%  
SET PubDB = AdventureWorks2012   
SET SubDB = AdventureWorks2012Replica   
SET PubName = AdvWorksSalesPersonMerge   
SET SnapshotDir=\\%DistPub%\repldata\unc\fernando  
  
"C:\Program Files\Microsoft SQL Server\120\COM\REPLMERG.EXE" -Publisher  %Publisher%    
-Subscriber  %Subscriber%  -Distributor %Publisher%  -PublisherDB %PubDB%    
-SubscriberDB %SubDB% -Publication %PubName%  -PublisherSecurityMode 1  -OutputVerboseLevel 3    
-Output -SubscriberSecurityMode 1  -SubscriptionType 3 -DistributorSecurityMode 1    
-Hostname "adventure-works\Fernando"  -DynamicSnapshotLocation %SnapshotDir%  
  
PAUSE  
  
```  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Puede utilizar Replication Management Objects (RMO) para generar mediante programación instantáneas con particiones de las maneras siguientes:  
  
-   Permita a los suscriptores que soliciten la generación y aplicación de instantáneas la primera vez que se sincronicen.  
  
-   Genere previamente las instantáneas para cada partición.  
  
-   Genere manualmente una instantánea para cada suscriptor ejecutando el Agente de instantáneas.  
  
> [!NOTE]  
>  Cuando el filtrado para un artículo produce particiones no superpuestas que son únicas para cada suscripción (especificando un valor de F:Microsoft.SqlServer.Replication.PartitionOptions.NonOverlappingSingleSubscription para P:Microsoft.SqlServer.Replication.MergeArticle.PartitionOption al crear un artículo de mezcla), los metadatos se limpian cada vez que se ejecuta el agente de mezcla. Esto significa que la instantánea con particiones expira antes. Cuando utilice esta opción, puede ser conveniente permitir a los suscriptores que soliciten la generación de instantáneas. Para obtener más información, vea la sección Usar las opciones de filtrado apropiadas del tema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar credenciales, use los [servicios de cifrado](http://go.microsoft.com/fwlink/?LinkId=34733) (en inglés) proporcionados por [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows .NET Framework.  
  
#### Para crear una publicación que permita a los suscriptores iniciar la generación y entrega de instantáneas  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> de clases para la base de datos de publicación, establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la instancia de <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 y la llamada la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> (método). Si <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> devuelve **false**, confirme que existe la base de datos.  
  
3.  Si <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> propiedad es **false**, establézcalo en **true** y llame a <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>.  
  
4.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase y establezca las siguientes propiedades para este objeto:  
  
    -   El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del paso 1 para <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>.  
  
    -   El nombre de la base de datos publicada <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>.  
  
    -   Un nombre para la publicación para <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>.  
  
    -   El número máximo de trabajos de instantáneas dinámicas para ejecutar para <xref:Microsoft.SqlServer.Replication.MergePublication.MaxConcurrentDynamicSnapshots%2A>. Dado que las solicitudes de instantáneas iniciadas por el suscriptor pueden producirse en cualquier momento, esta propiedad limita el número de trabajos del Agente de instantáneas que se pueden ejecutar simultáneamente cuando varios suscriptores solicitan al mismo tiempo su instantánea con particiones. Cuando se está ejecutando el número máximo de trabajos, las demás solicitudes de instantáneas con particiones se ponen en la cola hasta que se completa uno de los trabajos en ejecución.  
  
    -   Utilice el operador lógico OR bit a bit (**|** en Visual C# y **o** en Visual Basic) para agregar el valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowSubscriberInitiatedSnapshot> a <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
    -   La <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> y <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> campos de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> para proporcionar las credenciales para el [!INCLUDE[msCoName](../../includes/msconame-md.md)] de cuenta de Windows en la que se ejecuta el trabajo del agente de instantáneas.  
  
        > [!NOTE]  
        >  Configuración de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> se recomienda cuando se crea la publicación por un miembro de la **sysadmin** rol fijo de servidor. Para más información, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
5.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método para crear la publicación.  
  
    > [!IMPORTANT]  
    >  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todas las propiedades, incluyendo <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, se envían al distribuidor como texto sin formato. Debe cifrar la conexión entre el publicador y el distribuidor remoto antes de llamar a la <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> método. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
6.  Utilice la <xref:Microsoft.SqlServer.Replication.MergeArticle> propiedad para agregar artículos a la publicación. Especifique el <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propiedad para al menos un artículo que define el filtro con parámetros. (Opcional) Crear <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objetos que definen los filtros de combinación entre artículos. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
7.  Si el valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> es **false**, llame a <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para crear el trabajo inicial del agente de instantáneas para esta publicación.  
  
8.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método de la <xref:Microsoft.SqlServer.Replication.MergePublication> objeto creado en el paso 4. Esto inicia el trabajo de agente que genera la instantánea inicial. Para obtener más información sobre cómo generar una instantánea inicial y definir una programación personalizada para el Agente de instantáneas, vea [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
9. (Opcional) Comprobar un valor de **true** para el <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> propiedad para determinar cuándo está lista para usarse la instantánea inicial.  
  
10. Cuando el Agente de mezcla de un suscriptor se conecta por primera vez, se genera automáticamente una instantánea con particiones.  
  
#### Para crear una publicación y pregenerar o actualizar automáticamente las instantáneas  
  
1.  Usar una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase para definir una publicación de mezcla. Para obtener más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Utilice la <xref:Microsoft.SqlServer.Replication.MergeArticle> propiedad para agregar artículos a la publicación. Especifique el <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propiedad para al menos un artículo que define el filtro con parámetros y cree <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objetos que definen los filtros de combinación entre artículos. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Si el valor de <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> es **false**, llame a <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> para crear el trabajo del agente de instantáneas para esta publicación.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> método de la <xref:Microsoft.SqlServer.Replication.MergePublication> objeto creado en el paso 1. Este método inicia el trabajo de agente que genera la instantánea inicial. Para obtener más información sobre cómo generar una instantánea inicial y definir una programación personalizada para el Agente de instantáneas, vea [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
5.  Comprobar un valor de **true** para el <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> propiedad para determinar cuándo está lista para usarse la instantánea inicial.  
  
6.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePartition> clase y establezca los criterios de filtrado con parámetros para el suscriptor mediante una o ambas de las siguientes propiedades:  
  
    -   Si la partición del suscriptor se define por el resultado de [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), utilice <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A>.  
  
    -   Si la partición del suscriptor se define por el resultado de [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) o una sobrecarga de esta función, utilice <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A>.  
  
7.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> clase y establezca la misma propiedad como en el paso 6.  
  
8.  Utilice la <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> clase para definir una programación para generar la instantánea filtrada para la partición del suscriptor.  
  
9. La instancia de <xref:Microsoft.SqlServer.Replication.MergePublication> del paso 1, llame a <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergePartition%2A>. Pasar el <xref:Microsoft.SqlServer.Replication.MergePartition> objeto en el paso 6.  
  
10. La instancia de <xref:Microsoft.SqlServer.Replication.MergePublication> del paso 1, llame a la <xref:Microsoft.SqlServer.Replication.MergePublication.AddMergeDynamicSnapshotJob%2A> método. Pasar el <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> objeto del paso 7 y el <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule> objeto desde el paso 8.  
  
11. Llame a <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergeDynamicSnapshotJobs%2A>, y busque el <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob> objeto para el trabajo de instantánea con particiones recién agregado en la matriz devuelta.  
  
12. Obtener el <xref:Microsoft.SqlServer.Replication.MergeDynamicSnapshotJob.Name%2A> propiedad para el trabajo.  
  
13. Crear una conexión al distribuidor mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
14. Cree una instancia de SQL Server Management Objects (SMO) <xref:Microsoft.SqlServer.Management.Smo.Server> clase, pasando el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto del paso 13.  
  
15. Cree una instancia de la <xref:Microsoft.SqlServer.Management.Smo.Agent.Job> clase, pasando el <xref:Microsoft.SqlServer.Management.Smo.Server.JobServer%2A> propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server> objeto de paso 14 y el nombre del trabajo desde el paso 12.  
  
16. Llame a la <xref:Microsoft.SqlServer.Management.Smo.Agent.Job.Start%2A> método para iniciar el trabajo de instantánea con particiones.  
  
17. Repita los pasos 6-16 para cada suscriptor.  
  
#### Para crear una publicación y crear manualmente instantáneas para cada partición  
  
1.  Usar una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase para definir una publicación de mezcla. Para obtener más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Utilice la <xref:Microsoft.SqlServer.Replication.MergeArticle> propiedad para agregar artículos a la publicación, especifique la <xref:Microsoft.SqlServer.Replication.MergeArticle.FilterClause%2A> propiedad para al menos un artículo que define el filtro con parámetros y cree <xref:Microsoft.SqlServer.Replication.MergeJoinFilter> objetos que definen los filtros de combinación entre artículos. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Genere la instantánea inicial. Para más información, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
4.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> y establezca las propiedades necesarias siguientes:  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> : el nombre del publicador  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> : el nombre de la base de datos de publicación  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> : el nombre de la publicación  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> : el nombre del distribuidor  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> -un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> usa autenticación integrada de Windows o un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> utilizar autenticación de SQL Server.  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> -un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> usa autenticación integrada de Windows o un valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> utilizar autenticación de SQL Server.  
  
5.  Establecer un valor de <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> para <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>.  
  
6.  Establezca una o más de las propiedades siguientes para definir los parámetros del particionamiento:  
  
    -   Si la partición del suscriptor se define por el resultado de [SUSER_SNAME & #40; Transact-SQL & #41;](../../t-sql/functions/suser-sname-transact-sql.md), utilice <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterLogin%2A>.  
  
    -   Si la partición del suscriptor se define por el resultado de [HOST_NAME & #40; Transact-SQL & #41;](../../t-sql/functions/host-name-transact-sql.md) o una sobrecarga de esta función, utilice <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DynamicFilterHostName%2A>.  
  
7.  Llame al método <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> .  
  
8.  Repita los pasos 4-7 para cada suscriptor.  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 En este ejemplo se crea una publicación de combinación que permite a los suscriptores solicitar la generación de instantáneas.  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
 En este ejemplo se crea manualmente la partición del suscriptor y la instantánea filtrada para una publicación de combinación con filtros de filas con parámetros.  
  
 [!code-csharp[HowTo#rmo_CreateMergePartition](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepartition)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePartition](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepartition)]  
  
 En este ejemplo se inicia manualmente el Agente de instantáneas para generar la instantánea de datos filtrados de un suscriptor para una publicación de combinación con filtros de filas con parámetros.  
  
 [!code-csharp[HowTo#rmo_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_generatefilteredsnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateFilteredSnapshot](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_generatefilteredsnapshot)]  
  
## Vea también  
 [Filtros de fila con parámetros](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Instantáneas para publicaciones de combinación con filtros con parámetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  