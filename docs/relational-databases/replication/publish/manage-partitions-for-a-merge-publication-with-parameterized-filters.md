---
title: "Administrar particiones para una publicaci&#243;n de mezcla mediante filtros con par&#225;metros | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "particiones [replicación de SQL Server]"
  - "particiones de replicación de mezcla [replicación de SQL Server], SQL Server Management Studio"
  - "filtros con parámetros [replicación de SQL Server], administración de particiones"
ms.assetid: fb5566fe-58c5-48f7-8464-814ea78e6221
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Administrar particiones para una publicaci&#243;n de mezcla mediante filtros con par&#225;metros
  En este tema se describe cómo administrar particiones para una publicación de mezcla con filtros con parámetros en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] o Replication Management Objects (RMO). Los filtros de fila con parámetros se puede utilizar para generar particiones no superpuestas. Estas particiones pueden estar restringidas para que solo una suscripción reciba una partición determinada. En estos casos, un número grande de suscriptores producirá un número de particiones grande, las cuales a su vez requieren un número igual de instantánea con particiones. Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para administrar particiones para una publicación de mezcla mediante filtros con parámetros con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si genera un script para una topología de replicación (opción recomendada), los scripts de la publicación contienen las llamadas al procedimiento almacenado para crear particiones de datos. El script proporciona una referencia para las particiones creadas y una forma de volver a crear una o más divisiones en caso necesario. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
-   Cuando una publicación ha parametrizado filtros que producen suscripciones con particiones no superpuestas, y si una suscripción determinada se pierde y necesita volverse a crear, debe realizar las siguientes acciones: quitar la partición a la que se suscribió, volver a crear la suscripción y, a continuación, volver a crear la partición. Para más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md). La replicación genera scripts de creación para particiones del suscriptor existentes cuando se genera un script de creación de publicación. Para más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Administrar particiones en el **particiones de datos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). En esta página puede crear y eliminar particiones, permitir a los suscriptores iniciar la generación y distribución de instantáneas, generar instantáneas para una o más particiones, y limpiar instantáneas.  
  
#### Para crear una partición  
  
1.  En el **particiones de datos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Agregar**.  
  
2.  En el **Agregar partición de datos** cuadro de diálogo, escriba un valor para el **HOST_NAME ()** o **SUSER_SNAME ()** valor asociado a la partición que desea crear.  
  
3.  También puede especificar una programación para actualizar las instantáneas:  
  
    1.  Seleccione **programar el agente de instantáneas para esta partición se ejecute a las horas siguientes**  
  
    2.  Acepte la programación predeterminada para actualizar instantáneas o haga clic en **Cambiar** para especificar una programación diferente.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para eliminar una partición  
  
1.  En la página **Particiones de datos** , seleccione una partición en la cuadrícula.  
  
2.  Haga clic en **Eliminar**.  
  
#### Para permitir a los suscriptores inicializar la generación y distribución de instantáneas  
  
1.  En la página **Particiones de datos** , seleccione **Definir automáticamente una partición y generar una instantánea si es necesario cuando un suscriptor nuevo intente sincronizarse**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para generar una instantánea para una partición  
  
1.  En la página **Particiones de datos** , seleccione una partición en la cuadrícula.  
  
2.  Haga clic en **Generar instantáneas seleccionadas ahora**.  
  
#### Para limpiar una instantánea de una partición  
  
1.  En la página **Particiones de datos** , seleccione una partición en la cuadrícula.  
  
2.  Haga clic en **Limpiar instantáneas existentes**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Para administrar mejor una publicación con filtros parametrizados, puede enumerar mediante programación las particiones existentes utilizando los procedimientos almacenados de replicación. También puede crear y eliminar particiones existentes. Se puede obtener la información siguiente sobre las particiones existentes:  
  
-   Cómo se filtra una partición (con [SUSER_SNAME & #40; Transact-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md) o [HOST_NAME & #40; Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md)).  
  
-   El nombre del trabajo que genera una instantánea con particiones.  
  
-   La última vez que se ejecutó un trabajo de instantánea con particiones.  
  
 Mientras la segunda parte de la instantánea de dos partes se puede generar a petición cuando se inicializa una nueva suscripción, los procedimientos siguientes le permiten controlar cómo se genera esta instantánea y pre-generar dicha instantánea cuando sea más conveniente. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
#### Para ver información sobre particiones existentes  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergepartition & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md). Especifique el nombre de la publicación para **@publication**. (Opcional) Especifique **@suser_sname** o **@host_name** para devolver únicamente información basada en un único criterio de filtrado.  
  
#### Para definir una nueva partición y generar una nueva instantánea con particiones  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergepartition & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md). Especifique el nombre de la publicación para **@publication**y el valor con parámetros que define la partición para uno de los siguientes:  
  
    -   **@suser_sname** : cuando se define el filtro con parámetros mediante el valor devuelto por [SUSER_SNAME & #40; Transact-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md).  
  
    -   **@host_name** : cuando se define el filtro con parámetros mediante el valor devuelto por [HOST_NAME & #40; Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md).  
  
2.  Cree e inicialice la instantánea parametrizada para esta nueva partición. Para más información, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
#### Para eliminar una partición  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_dropmergepartition & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md). Especifique el nombre de la publicación para **@publication** y el valor con parámetros que define la partición para uno de los siguientes:  
  
    -   **@suser_sname** : cuando se define el filtro con parámetros mediante el valor devuelto por [SUSER_SNAME & #40; Transact-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md).  
  
    -   **@host_name** : cuando se define el filtro con parámetros mediante el valor devuelto por [HOST_NAME & #40; Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md).  
  
     Este procedimiento quita también el trabajo de instantáneas y los archivos de instantáneas de la partición.  
  
##  <a name="RMOProcedure"></a> Usar Replication Management Objects (RMO)  
 Para administrar mejor una publicación con filtros parametrizados, puede crear mediante programación nuevas particiones del suscriptor, enumerar las particiones del suscriptor existentes y eliminar las particiones del suscriptor utilizando Replication Management Objects (RMO). Para obtener más información acerca de cómo particiones del suscriptor, vea [Create a Snapshot for a Merge Publication with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). Se puede obtener la información siguiente sobre las particiones existentes:  
  
-   El valor y la función de filtrado en los que se basa la partición.  
  
-   El nombre del trabajo que genera una instantánea con parámetros para el suscriptor.  
  
-   La última vez que se ejecutó un trabajo de instantánea con parámetros.  
  
#### Para ver información sobre particiones existentes  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase. Establecer el <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> (método) y pasa el resultado a una matriz de <xref:Microsoft.SqlServer.Replication.MergePartition> objetos.  
  
5.  Para cada <xref:Microsoft.SqlServer.Replication.MergePartition> en la matriz de objetos, obtener las propiedades de interés.  
  
#### Para eliminar particiones existentes  
  
1.  Crear una conexión al publicador mediante la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> clase.  
  
2.  Cree una instancia de la <xref:Microsoft.SqlServer.Replication.MergePublication> clase. Establecer el <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Propiedades de la publicación y establezca el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad a la <xref:Microsoft.SqlServer.Management.Common.ServerConnection> creado en el paso 1.  
  
3.  Llame a la <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> método para obtener las propiedades del objeto. Si este método devuelve **false**, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  Llame a la <xref:Microsoft.SqlServer.Replication.MergePublication.EnumMergePartitions%2A> (método) y pasa el resultado a una matriz de <xref:Microsoft.SqlServer.Replication.MergePartition> objetos.  
  
5.  Para cada <xref:Microsoft.SqlServer.Replication.MergePartition> en la matriz de objetos, determinar si se debe eliminar la partición. Esta decisión normalmente se basa en el valor de la <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterLogin%2A> propiedad o <xref:Microsoft.SqlServer.Replication.MergePartition.DynamicFilterHostName%2A> propiedad.  
  
6.  Llame a la <xref:Microsoft.SqlServer.Replication.MergePublication.RemoveMergePartition%2A> método en el <xref:Microsoft.SqlServer.Replication.MergePublication> objeto desde el paso 2. Pasar el <xref:Microsoft.SqlServer.Replication.MergePartition> objeto del paso 5.  
  
7.  Repita el paso 6 para cada partición que se elimina.  
  
## Vea también  
 [Filtros de fila con parámetros](../../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Instantáneas para publicaciones de combinación con filtros con parámetros](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  